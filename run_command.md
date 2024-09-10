```
def run_local_command(cmd, check=True, output_cmd=True, output_result=True):
    if output_cmd:
        logger.info(f"Run local command `{cmd}`")
    try:
        res = subprocess.run(
            cmd,
            shell=True,
            check=check,
            encoding="utf-8",
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            env=dict(os.environ, LANG=SHELL_LANG),
        )
        if output_result:
            logger.info(
                f"Result errno: {res.returncode}\nstdout:\n{res.stdout}\nstderr:\n{res.stderr}"
            )
        return res
    except subprocess.CalledProcessError as exc:
        raise RuntimeError(
            f"Errno: {exc.returncode}\nstdout:\n{exc.stdout}\nstderr:\n{exc.stderr}"
        )
```


```
#     with subprocess.Popen(
#         inotifywait_cmd_list,
#         stdout=subprocess.PIPE,
#         universal_newlines=True,
#     ) as inotify_process:
#         for line in inotify_process.stdout:
#             logger.info(f"监控到文件变化：{line}")
#             *_, path = line.strip().strip("'").split(" ", 2)
#             # path: /volmountpoint/aiopool/305b81fb6fb8_0_71_1692358578_oceanbase/ob110145146147/1675402832/incarnation_1/1001/clog/27/data/1100611139404002/0/4
#
#             try:
#                 # 不够位的就跳过
#                 new_src_path_list = path.split(os.path.sep)[:9]  # 到 clog 目录
#                 logger.info(f"new_src_path_list: {new_src_path_list}")
#             except Exception:
#                 logger.info(f"{path} 不是 clog 目录，跳过")
```


