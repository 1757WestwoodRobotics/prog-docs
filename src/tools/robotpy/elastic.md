# Elastic

Elastic is a powerful open-source search and analytics engine that can be used for a variety of purposes, including logging and data analysis. In FRC, Elastic can be used to:

-   Log data from the robot for later analysis.
-   Create dashboards to visualize the robot's performance.
-   Identify trends and patterns in the robot's data.

Using Elastic for FRC is an advanced topic and requires setting up an ElasticSearch server to receive data. Data can be sent from the robot to the server via HTTP requests.

For more information, see the Elastic documentation: [https://www.elastic.co/guide/index.html](https://www.elastic.co/guide/index.html)

### Conceptual Example: Logging to Elastic

This example shows how you could create a logger class that sends data to an Elastic server. This requires the `requests` library to be installed on the robot (`pip install requests`).

```python
import requests
import json
import datetime

class ElasticLogger:
    def __init__(self, elastic_url, index_name):
        self.elastic_url = elastic_url
        self.index_name = index_name

    def log(self, message, level="info"):
        timestamp = datetime.datetime.utcnow().isoformat()
        document = {
            "message": message,
            "level": level,
            "@timestamp": timestamp,
        }
        try:
            response = requests.post(
                f"{self.elastic_url}/{self.index_name}/_doc",
                headers={"Content-Type": "application/json"},
                data=json.dumps(document),
                timeout=0.5 # Use a short timeout to avoid blocking robot code
            )
            response.raise_for_status()
        except requests.exceptions.RequestException as e:
            print(f"Error logging to Elastic: {e}")

# Example usage in a robot:
# In robotInit():
# self.logger = ElasticLogger("http://your-elastic-server:9200", "robot-logs")
# self.logger.log("Robot initialized")

# In autonomousInit():
# self.logger.log("Autonomous enabled")
```
