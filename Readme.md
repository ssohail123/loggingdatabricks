# Logging in Databricks Application

## Overview  
This project demonstrates effective and contextual logging within a Databricks notebook. It includes custom log formatters, integration with Databricks utilities to enrich log messages with workspace and notebook metadata, file-based log management, and robust error handling.

## Features

### Notebook Context Logging  
- Dynamically captures the notebook name and workspace context using `dbutils`.
- This metadata is included in every log message to make logs easier to trace back to their execution context.

### Custom Log Formatters  
Two log format styles were tested to determine the most informative and readable format:
1. Function-oriented: includes function name, logger name, and timestamp.
2. File and line-oriented: includes filename, line number, and log level.

This flexibility helps tailor logs to different debugging needs.

### Timestamped Log Files  
- Logs are saved in `/tmp/logs/` with filenames based on the current date and hour (e.g., `2025-05-26-15.log`).
- This hourly naming convention avoids overwriting, supports better log rotation, and makes searching specific logs easier.

### Logger Setup  
- A named logger (`log4j`) is initialized with `DEBUG` level for detailed logging.
- FileHandler writes logs to hourly timestamped files using the selected formatter.
- Notebook and workspace details are consistently included in the log context.

### PySpark Data Processing  
- Reads a sample CSV file (`BigMart_Sales.csv`) using Spark.
- Logs are written at the start of the read and after counting the number of records.

### Error Handling and Logging  
- A controlled error is introduced by accessing a non-existent DataFrame column.
- The exception is caught and logged using `logger.error()` to verify error tracking.

### Logging Levels  
- `INFO` is used for major process steps and status updates.
- `ERROR` is used to capture unexpected behavior and issues.

### Graceful Logging Finalization  
- `logging.shutdown()` ensures all log entries are flushed and written before the script ends.

### Logging Best Practices Followed  
- Log folder is created if missing using `os.makedirs()`.
- Duplicate logs are avoided by careful handler management.
- Hour-based log filenames ensure clarity and make logs easier to correlate with runtime activity.

## Summary  
This setup emphasizes clarity, traceability, and practical debugging in Databricks. By logging both the workspace and notebook name, each log message carries full execution context. Combined with hourly log file naming, this makes it easy to isolate issues, search logs quickly, and avoid confusion across different runs. This level of structured, contextual logging reflects a specialty in building systems that are not only functional but easy to operate and debug in production environments.

