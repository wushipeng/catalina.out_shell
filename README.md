# catalina.out_shell
这个是只保存catalina最近一周的日志脚本

#!/bin/bash 
#it's to delete the log that before in the 7 days
#2015-05-23

read -p "Please input y or n (`echo -e "\033[33mY/y\033[0m"`: `echo -e "\033[32mdelete the catalina.out before 7 days\033[0m"`  `echo -e "\033[33mN/n\033[0m"`: `echo -e "\033[32m exit\033[0m"`):" result
case $result in
Y|y)

a=`date +"%Y-%m-%d" -d" -7 day"`
b=`grep -n  $a catalina.out |  awk -F ':' '{print $1}' | sed -n '1p'`
c=$((b-1))

d=`date +"%b %d,%Y" -d "-7 day"`
e=`grep -n  "$d" catalina.out |  awk -F ':' '{print $1}' | sed -n '1p'`
f=$((e-1))




if [ $c -gt 0 ]
                then
                if [ $f -gt 0 ]
                                then

                                if [ $c -lt $f ]
                                                then

                                                sed -i "1,"$c"d" catalina.out
                                                echo -e "\033[31mdelete the log successful  \033[0m"
                                else
                                                sed -i "1,"$f"d" catalina.out
                                                echo -e "\033[31mdelete the log successful  \033[0m"

                                fi
                elif [ $f -eq 0 ]
                                then
                                exit 0

                else

                                sed -i "1,"$c"d" catalina.out
                fi
elif [ $f -gt 0 ]
                then
                if [ $c -eq 0 ]
                        then
                                exit 0
                        else

                        sed -i "1,"$f"d" catalina.out
                        echo -e "\033[31mdelete the log successful  \033[0m"
                fi


else

                        echo -e "|\033[47;31mno lines to delete\033[0m|"

fi
;;
N|n)
        exit 0
esac

