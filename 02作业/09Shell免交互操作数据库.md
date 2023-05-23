# Shell免交互操作数据库

```shell
#!/bin/bash

declare -r script_name=$(echo ${0##*/})
declare -r run_dir=$(dirname $(readlink -f $0))
function check_env()
{   
    # check basic component environment
    base_dir=${BASE_HOME}
    base_dir=`echo ${base_dir%*/}`
    base_shell_dir="${base_dir}/stanlong/scripts"
    base_conf_dir="${base_dir}/stanlong/conf"
    cluster_conf="${base_conf_dir}/cluster.conf"
    source ${cluster_conf}
}

function nossh()
{
	#log_debug "nsssh $@"
	declare -r host=$(echo $1 | cut -s -d'@' -f2-)
	declare -r user=$(echo $1 | cut -s -d'@' -f1)
	declare -r passwd=$2
	shift 2

	cmmand=$@
	
	mkdir -p $run_dir/pass
	chmod 0700 $run_dir/pass
	echo -e "#!/bin/bash\necho '$passwd'" >$run_dir/pass/${host}_$user
	chmod 0700 $run_dir/pass/${host}_$user
	export SSH_ASKPASS=$run_dir/pass/${host}_$user
	export	 DISPLAY='none:0'
	setsid ssh $user@$host		-o UserKnownHostsFile=$run_dir/pass/known_hosts -o StrictHostKeyChecking=no -o LogLevel=ERROR  $cmmand	
	rm -rf $run_dir/pass
}

function update_schema(){


	declare -r UH=$stanlong_database_server_user@$stanlong_database_server_host
	nossh $UH $stanlong_database_server_pass '$ORACLE_HOME'/bin/sqlplus -L \
			$stanlong_database_username/$stanlong_database_password@$stanlong_database_server_host:$stanlong_database_server_port/$stanlong_database_name \
			< $run_dir/update.sql
	# nossh $stanlong_database_server_user@$stanlong_database_server_host $stanlong_database_server_pass id
}

check_env
update_schema[hadoop@node01 stanlong_update_script]$ 
```

