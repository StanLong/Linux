# 统计活跃用户CPU使用率

```shell
#!/bin/bash
echo "User          CPU Usage (%)"
echo "---------------------------"

ps -eo user,%cpu,comm,maj_flt,rss | awk '
    NR > 1 {
        cpu[$1] += $2
    }
    END {
        for (user in cpu) {
            printf("%-16s %.2f\n", user, cpu[user] )
        }
    }
' | sort -k2 -rn
```

