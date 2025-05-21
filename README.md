# 📦 Sales Data Pipeline

This project demonstrates a complete sales data pipeline using **Apache NiFi**, **Docker**, **Elasticsearch**, and **Kibana**. The pipeline ingests sales data from a CSV file, transforms it in NiFi, stores it in Elasticsearch, and visualizes it with Kibana.

---

## 🚀 Architecture

- **Apache NiFi**: For ingesting and transforming sales data from CSV
- **Docker**: For containerized deployment of all services
- **Elasticsearch**: For indexing and storing structured data
- **Kibana**: For visualizing sales insights

---

## 📂 Project Structure

```
sales-data-pipeline/
│
├── data/
│   └── sales_data_sample.csv            # Raw CSV data
│
├── docker/
│   ├── docker-compose.yml               # Docker setup for all services
│   └── nifi/
│       └── (optional NiFi config files)
│
├── nifi/
│   └── templates/
│       └── sales-pipeline-template.xml  # Exported NiFi flow template
│
├── notebooks/
│   └── data_template.ipynb              # Preview and test data
│
├── README.md                            # Project documentation
│
└── .gitignore                           # Ignore temp and sensitive files
```

---

## 🛠 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/MenghoutChhon/sales-data-pipeline.git
   cd sales-data-pipeline
   ```

2. **Start the services using Docker Compose**
   ```bash
   cd docker
   docker-compose up -d
   ```

3. **Access the services**
   - NiFi: [http://localhost:8080/nifi](http://localhost:8080/nifi)
   - Kibana: [http://localhost:5601](http://localhost:5601)
   - Elasticsearch: [http://localhost:9200](http://localhost:9200)

4. **Import NiFi flow**
   - Go to NiFi UI
   - Upload the template from `nifi/templates/sales-pipeline-template.xml`
   - Deploy the flow and run it

---

## 📥 Sample Data Input

The input data is located in `data/sales_data_sample.csv`. This file contains sales transactions including:
- Order Number
- Product Code
- Quantity Ordered
- Price Each
- Order Date
- Customer Info

---

## 🐳 Docker Setup

Here’s the full `docker-compose.yml` used in the project:

```yaml
version: '3.8'

services:
  nifi:
    image: apache/nifi:latest
    container_name: nifi
    ports:
      - "8080:8080"
    environment:
      - NIFI_WEB_HTTP_PORT=8080
    restart: unless-stopped

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.17.3
    container_name: elasticsearch
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
    ports:
      - "9200:9200"
    restart: unless-stopped

  kibana:
    image: docker.elastic.co/kibana/kibana:7.17.3
    container_name: kibana
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch
    restart: unless-stopped
```

---

## 📊 Kibana Dashboard Ideas

Once the data is in Elasticsearch, you can build dashboards in Kibana such as:

- 💰 **Total Revenue by Country**
- 📦 **Top Selling Products**
- 📈 **Sales Trend Over Time**
- 📍 **Sales by Customer Location**

---

## 📓 Jupyter Notebook

Use `notebooks/data_template.ipynb` to:
- Preview data
- Clean or validate before sending it into NiFi

Example:
```python
import pandas as pd
df = pd.read_csv('../data/sales_data_sample.csv')
print(df.head())
```

---

## 📌 Author

**Menghout Chhon**  
Data Science Student | [GitHub Profile](https://github.com/MenghoutChhon)

---

## 🪪 License

This project is open-source and available under the MIT License.
