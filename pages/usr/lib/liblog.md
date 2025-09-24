# liblog
A basic logging library

## Types
* The different types of logging severity
    ```c
    typedef enum { 
        LOG_DEBUG, 
        LOG_INFO, 
        LOG_WARN, 
        LOG_ERROR 
    } log_level_t;
    ```

## Functions
* Sets up the logging library. If not called, `file` is set to `/log/unknown.log`, and `level` is set to `LOG_INFO`
    ```c
    void log_init(const char* file, const log_level_t level);
    ```
* Writes a formatted string, along with timestamp and colour-coded log level
    ```c
    void log_console_level(log_level_t level, const char *fmt, ...);
    ```

## Macros
* Wrappers for `log_console_level()`, automatically inputting the correct log level
    ```c
    #define log_debug(fmt, ...) log_console_level(LOG_DEBUG, fmt, ##__VA_ARGS__)
    #define log_info(fmt, ...)  log_console_level(LOG_INFO, fmt, ##__VA_ARGS__)
    #define log_warn(fmt, ...)  log_console_level(LOG_WARN, fmt, ##__VA_ARGS__)
    #define log_error(fmt, ...) log_console_level(LOG_ERROR, fmt, ##__VA_ARGS__)
    ```
* Wrapper for `log_error`, formatted like `perror()`
    ```c
    #define log_perror(err) log_console_level(LOG_ERROR, "%s: %s\n", err, strerror(errno))
    ```

## Variables
* Current set minimum level to log. If you attempt to log using a level lower than this, it is ignored.
    ```c
    extern int loglevel;
    ```
* Current set outputted logging file.
    ```c
    extern char* logfile;
    ```