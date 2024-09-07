import os
print(dir(os))
#
dir shows all the attribute and methods within os module
```
['CLD_CONTINUED', 'CLD_DUMPED', 'CLD_EXITED', 'CLD_KILLED', 'CLD_STOPPED', 'CLD_TRAPPED', 'DirEntry', 'EX_CANTCREAT', 'EX_CONFIG', 'EX_DATAERR', 'EX_IOERR',
'EX_NOHOST', 'EX_NOINPUT', 'EX_NOPERM', 'EX_NOUSER', 'EX_OK', 'EX_OSERR', 'EX_OSFILE', 'EX_PROTOCOL', 'EX_SOFTWARE', 'EX_TEMPFAIL', 'EX_UNAVAILABLE', 'EX_USAGE', 'F_LOCK', 'F_OK', 'F_TEST', 'F_TLOCK', 'F_ULOCK', 'GenericAlias', 'Mapping', 'MutableMapping', 'NGROUPS_MAX', 'O_ACCMODE', 'O_APPEND', 'O_ASYNC', 'O_CLOEXEC', 'O_CREAT', 'O_DIRECT', 'O_DIRECTORY', 'O_DSYNC', 'O_EXCL', 'O_EXEC', 'O_LARGEFILE', 'O_NDELAY', 'O_NOATIME', 'O_NOCTTY', 'O_NOFOLLOW', 'O_NONBLOCK', 'O_PATH', 'O_RDONLY', 'O_RDWR', 'O_RSYNC', 'O_SEARCH', 'O_SYNC', 'O_TMPFILE', 'O_TRUNC', 'O_TTY_INIT', 'O_WRONLY', 'POSIX_FADV_DONTNEED', 'POSIX_FADV_NOREUSE', 'POSIX_FADV_NORMAL', 'POSIX_FADV_RANDOM', 'POSIX_FADV_SEQUENTIAL', 'POSIX_FADV_WILLNEED', 'PRIO_PGRP', 'PRIO_PROCESS', 'PRIO_USER', 'P_ALL', 'P_NOWAIT', 'P_NOWAITO', 'P_PGID', 'P_PID', 'P_WAIT', 'PathLike', 'RTLD_GLOBAL', 'RTLD_LAZY', 'RTLD_LOCAL', 'RTLD_NODELETE', 'RTLD_NOLOAD', 'RTLD_NOW', 'R_OK', 'SCHED_BATCH', 'SCHED_FIFO', 'SCHED_IDLE', 'SCHED_OTHER', 'SCHED_RESET_ON_FORK', 'SCHED_RR', 'SEEK_CUR', 'SEEK_END', 'SEEK_SET', 'ST_APPEND', 'ST_MANDLOCK', 'ST_NOATIME', 'ST_NODEV', 'ST_NODIRATIME', 'ST_NOEXEC', 'ST_NOSUID', 'ST_RDONLY', 'ST_RELATIME', 'ST_SYNCHRONOUS', 'ST_WRITE', 'TMP_MAX', 'WCONTINUED', 'WCOREDUMP', 'WEXITED', 'WEXITSTATUS', 'WIFCONTINUED', 'WIFEXITED', 'WIFSIGNALED', 'WIFSTOPPED', 'WNOHANG', 'WNOWAIT', 'WSTOPPED', 'WSTOPSIG', 'WTERMSIG', 'WUNTRACED', 'W_OK', 'X_OK', '_Environ', '__all__', '__builtins__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_check_methods', '_execvpe', '_exists', '_exit', '_fspath', '_fwalk', '_get_exports_list', '_spawnvef', '_wrap_close', 'abc', 'abort', 'access', 'altsep', 'chdir', 'chmod', 'chown', 'chroot', 'close', 'closerange', 'confstr', 'confstr_names', 'cpu_count', 'ctermid', 'curdir', 'defpath', 'device_encoding', 'devnull', 'dup', 'dup2', 'environ', 'environb', 'error', 'execl', 'execle', 'execlp', 'execlpe', 'execv', 'execve', 'execvp', 'execvpe', 'extsep', 'fchdir', 'fchmod', 'fchown', 'fdatasync', 'fdopen', 'fork', 'fpathconf', 'fsdecode', 'fsencode', 'fspath', 'fstat', 'fstatvfs', 'fsync', 'ftruncate', 'fwalk', 'get_blocking', 'get_exec_path', 'get_inheritable', 'getcwd', 'getcwdb', 'getenv', 'getenvb', 'getgid', 'getloadavg', 'getlogin', 'getpgid', 'getpgrp', 'getpid', 'getppid', 'getpriority', 'getsid', 'getuid', 'isatty', 'kill', 'killpg', 'linesep', 'listdir', 'lockf', 'login_tty', 'lseek', 'lstat', 'major', 'makedev', 'makedirs', 'minor', 'mkdir', 'name', 'open', 'pardir', 'path', 'pathconf', 'pathconf_names', 'pathsep', 'pipe', 'popen', 'posix_fadvise', 'pread', 'putenv', 'pwrite', 'read', 'readlink', 'readv', 'register_at_fork', 'remove', 'removedirs', 'rename', 'renames', 'replace', 'rmdir', 'scandir', 'sched_yield', 'sep', 'set_blocking', 'set_inheritable', 'setgid', 'setpgid', 'setpgrp', 'setregid', 'setreuid', 'setsid', 'setuid', 'spawnl', 'spawnle', 'spawnlp', 'spawnlpe', 'spawnv', 'spawnve', 'spawnvp', 'spawnvpe', 'st', 'stat', 'stat_result', 'statvfs', 'statvfs_result', 'strerror', 'supports_bytes_environ', 'supports_dir_fd', 'supports_effective_ids', 'supports_fd', 'supports_follow_symlinks', 'symlink', 'sync', 'sys', 'sysconf', 'sysconf_names', 'system', 'tcgetpgrp', 'tcsetpgrp', 'terminal_size', 'times', 'times_result', 'truncate', 'ttyname', 'umask', 'uname', 'uname_result', 'unlink', 'unsetenv', 'urandom', 'utime', 'wait', 'waitid', 'waitid_result', 'waitpid', 'waitstatus_to_exitcode', 'walk', 'write', 'writev']
>>> 

```

Current working directory:
```
 import os
 print(os.getcwd()) # /Users/surkohli/Desktop

 os.chdir('/Users/surkohli')
 print(os.getcwd()) # /Users/surkohli
 print(os.listdir()) # to list all folders and files on current path
 output:
 ['.config', 'Music', '.condarc', '.docker', '.DS_Store', '.CFUserTextEncoding', '.xonshrc', '.zshrc', 'Environments', 'Pictures', '.zprofile', '.nvm', 'Postman',
 '.zsh_history', '.ipython', 'Desktop', 'Library', '.vpn', '.lesshst', '.duoconnect', '.ddi_cache', 'testing', 'Public', '.tcshrc', '.cisco', 'OneDrive - Cisco', 
 '.anaconda', '.ssh', 'Movies', 'Applications', '.profile', '.Trash', '.jupyter', '.zcompdump', '.ddi_scratch', 'Documents', '.pyenv', '.vscode', '.bash_profile',
 'Downloads', '.python_history', '.continuum', '.cache', '.aws', '.gitconfig', '.viminfo', '.zsh_sessions', '.conda', 'src']

#You can also pass a path in listdir to list all files folders in a path

Now what if u want to create a folder, u have 2 funcs: mkdir() and makedirs() but os.makedirs(<dirname>) can make directories recursively ie it can create sub directories
os.mkdir('OS-Module-Demo') # Creates a folder named OS-Module-Demo in the current path
os.makedirs('OS-Top-Level/OS-Nested-Level') # it will crreate top level dir if it does not exists and also will create sub dir

if we want to delete folders: rmdir() and
 removedirs() # deletes directories recursively
```
 
