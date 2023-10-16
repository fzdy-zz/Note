Ubuntu Jammy SSH 登录遇到
Access denied
经查service sshd status
PAM unable to dlopen(pam_tally2.so): /lib/security/pam_tally2.so: cannot open shared object file: No such file or directory
PAM adding faulty module: pam_tally2.so



Ubuntu 22.04系统中 pam_tally2.so 这个模块已经不再被使用，
需要使用pam_faillock.so来代替，
但是PAM文件中默认还是在使用pam_tally2.so ，这里就需要手动修改etc/pam.d/sshd中的
auth required pam_tally2.so deny=3 unlock_time=300 even_deny_root root_unlock_time=300
改为
auth required pam_faillock.so deny=3 unlock_time=300 even_deny_root root_unlock_time=300
