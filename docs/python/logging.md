### Typical config
Taken from [here](https://fangpenlin.com/posts/2012/08/26/good-logging-practice-in-python/)
```python
import logging, logging.config
def setup_logging(
    default_path='logging.yaml',
    default_level=logging.INFO,
    env_key='LOG_CFG'
    ):
    """Setup logging configuration

    """
    path = default_path
    value = os.getenv(env_key, None)
    if value:
        path = value
    if os.path.exists(path):
        with open(path, 'rt') as f:
            config = yaml.safe_load(f.read())
        logging.config.dictConfig(config)
    else:
        logging.basicConfig(level=default_level)
```

`logging.yaml` could be something like

```yaml
---
version: 1
disable_existing_loggers: False
formatters:
    simple:
        format: "%(asctime)s - %(name)s - %(levelname)s - %(message)s"

handlers:
    console:
        class: logging.StreamHandler
        level: INFO
        formatter: simple
        stream: ext://sys.stdout

    info_file_handler:
        class: logging.handlers.RotatingFileHandler
        level: INFO
        formatter: simple
        filename: logs/info.log
        maxBytes: 2097152 # 2MB
        backupCount: 20
        encoding: utf8

    debug_file_handler:
        class: logging.handlers.RotatingFileHandler
        level: DEBUG
        formatter: simple
        filename: logs/debug.log
        maxBytes: 2097152 # 2MB
        backupCount: 20
        encoding: utf8

    error_file_handler:
        class: logging.handlers.RotatingFileHandler
        level: ERROR
        formatter: simple
        filename: logs/errors.log
        maxBytes: 10485760 # 10MB
        backupCount: 20
        encoding: utf8

loggers:
    get_transactions:
        level: ERROR
        handlers: [console]
        propagate: no

root:
    level: DEBUG
    handlers: [console, debug_file_handler, info_file_handler, error_file_handler]
```


Can be used like this
```python
import logging
from utils import setup_logging

setup_logging(default_path="./logging_some_module.yaml")
logger = logging.getLogger(__name__)

# sets level for the urllib3 module to WARNING
logging.getLogger("urllib3").setLevel(logging.WARNING)
```
