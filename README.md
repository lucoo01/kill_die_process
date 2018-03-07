# kill_die_process 定时清除 超时的进程

## crontab -e
```
0 */1 * * * source /crontab/kill_die_process.sh
```
----
kill_die_process.sh
```sh
pids=`ps aux | grep /root/soft/docker/  | grep -v grep | awk '{print $2}'`
for x in $pids;do
        times=`ps -p $x -o etimes=`
        if [ $[$times] -gt 1000 ];then
                kill -9 $x;
                #echo $times;
                echo "$x is killed!!";
        fi
done
```
以上清除运行超过 1000 秒 (有些用户会写死循环)
