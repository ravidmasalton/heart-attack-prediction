# heart-attack-prediction

Real-time heart attack prediction system using Streamlit, Kafka, Spark, and Machine Learning.

## 🎯 Project Goal
Build a system that:
- Accepts clinical data input via a Streamlit web UI
- Sends data to a Kafka topic for prediction
- Consumes and processes predictions using Apache Spark
- Uses a trained ML model to assess heart attack risk

## 🧠 Technologies Used
- **Languages**: Python
- **Web UI**: Streamlit
- **Machine Learning**: scikit-learn, NumPy, Pandas
- **Deep Learning**: PyTorch, TensorFlow
- **Big Data**: Apache Spark
- **Messaging**: Apache Kafka
- **Data Processing**: JSON, Kafka Streams

## 📁 Project Structure
- `app.py` - Streamlit app for user input and prediction visualization
- `Heart Consumer.ipynb` - Spark consumer for real-time prediction handling
- `data_heart producer.ipynb` - Kafka producer simulator (optional)
- `heart_disease_uci.csv` - Dataset used for model training
- `config.txt` - Configuration settings and execution commands
- 
## ▶️ How to Run

### 1. Install Dependencies
```bash
pip install streamlit
```

### 2. Start Kafka Services
```bash
bin/zookeeper-server-start.sh config/zookeeper.properties &
bin/kafka-server-start.sh config/server.properties &
```

### 3. Create Kafka Topics
```bash
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic heart_data
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic prediction
```

### 4. Run All Notebooks
Run the following notebooks in order to simulate data streaming and processing:

- `data_heart producer.ipynb` – simulates sending heart data to Kafka
- `Heart Consumer.ipynb` – consumes and processes predictions from Kafka

## 📌 Notes
- Input features include: Age, Sex, CP, Trestbps, Chol, FBS, RestECG, Thalch, Exang, Oldpeak
- Kafka topics: `test` (input), `prediction` (output), `heart_data` (raw data ingestion)

### 5. Convert and Run Streamlit App
```bash
jupyter nbconvert --to script app.ipynb
streamlit run app.py
```
## 📈 Model Performance
We trained a machine learning model using the UCI Heart Disease dataset.
- **Accuracy Achieved**: ~82%
- The model was evaluated using standard cross-validation techniques.

## 🚀 Execution Summary
To run the full pipeline, make sure to execute the following files:
1. `data_heart producer.ipynb` – streams clinical data to Kafka
2. `Heart Consumer.ipynb` – consumes data and predictions using Spark
3. `app.py` – provides a real-time web interface for input and prediction display
