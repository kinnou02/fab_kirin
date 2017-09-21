# fab_kirin
Kirin's deployment mechanisms

## deployment files

File should look like:

```python
from fabric.api import *
import common


def prod():
    env.name = 'prod'

    env.roledefs = {
        'kirin': ['<user>@<kirin_platform1>', '<user>@<kirin_platform2>'],
        'kirin-beat': ['<user>@<kirin-beat_platform>'] #only one beat can exist
    }

    env.kirin_host = '<kirin_host_name>'

    env.previous_docker_tag = '<prev_tag>'
    env.current_docker_tag = '<prod_tag>'

    env.use_load_balancer = True #or False

    env.postgres_database = '<SQL_db_platform>'
    env.navitia_url = 'https://api.navitia.io'
    env.navitia_token = '<sncf-access-token>'
    env.rabbitmq_url = '<rabbitmq_platform>' #rabbitmq where disruptions are published for navitia

    env.navitia_gtfs_rt_instance = 'ca-qc-sherbrooke' #sherbrooke coverage name
    env.navitia_gtfs_rt_token = '<sherbrooke-access-token>'
    env.gtfs_rt_contributor = 'realtime.sherbrooke' #rabbitmq topic, to match with rt_topics in kraken.ini (and is_realtime_enabled=True)
    env.gtfs_rt_feed_url = 'http://<sherbrooke-url>/tripUpdates.pb' url of sherbrooke trip update protobuf

    env.celery_broker_url = 'pyamqp://<user>:<mdp>@<platform>:<port>/<vhost>?heartbeat=60' #beware to open access to vhost for user in rabbitmq (for beat-worker communication)

    env.use_logger = True
```
