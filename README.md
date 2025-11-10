# Basic-Programming
# logger_util.py

import datetime
import os

class Logger:
    def __init__(self, logfile: str = "app.log"):
        self.logfile = logfile
        # Ensure log directory exists
        logdir = os.path.dirname(self.logfile)
        if logdir and not os.path.exists(logdir):
            os.makedirs(logdir)

    def _write(self, level: str, message: str):
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        log_entry = f"[{timestamp}] [{level}] {message}\n"
        with open(self.logfile, "a", encoding="utf-8") as f:
            f.write(log_entry)

    def info(self, message: str):
        self._write("INFO", message)

    def warning(self, message: str):
        self._write("WARNING", message)

    def error(self, message: str):
        self._write("ERROR", message)

if __name__ == "__main__":
    logger = Logger("logs/my_app.log")
    logger.info("Application started")
    logger.warning("This is a warning example")
    logger.error("This is an error example")
    print("Logging done, check logs/my_app.log")
