# ai-for-good
1. Project Title
“AI-Enabled Tecmos Mursik Palace: Empowering Traditional Dairy Sustainability through Smart Supply Chain (SDG 2 & SDG 8)”

2. SDG Focus
Goal:

SDG 2: Zero Hunger

SDG 8: Decent Work and Economic Growth

Problem:
Traditional fermented milk producers in Kenya (e.g., Mursik) lack digital tools to manage demand forecasting, inventory, spoilage risks, and market trends. This leads to product waste, income instability, and missed sales opportunities.

3. AI Approach
Software Engineering Skills Applied:

Automation:
Use machine learning to automate supply-demand forecasting, inventory alerts, and consumer preference trends.

Testing:
Apply unit tests for API functions and integration tests across ordering, delivery, and alerts modules.

Scalability:
Design modular and API-driven architecture for mobile and web platforms, scalable for rural and urban use.

Technical Solution:

Train a time series ML model to forecast daily demand and expiration risks.

Use image classification AI to assess quality/freshness from vendor uploads.

Use recommendation engine for customers (e.g., recipe pairings, order history).

NLP-powered chatbot to educate farmers and users on safe milk handling.

4. Tools & Frameworks
AI/ML: Scikit-learn, TensorFlow Lite (for mobile), OpenCV (image quality analysis)

Software Engineering:
GitHub (code hosting), Git for versioning, Docker for containerized deployment, Streamlit for admin dashboard

CI/CD: GitHub Actions or GitLab Pipelines

Data Sources:

Internal product sales history

Public agriculture datasets from FAO or Kenya Open Data

Mobile-collected survey data

5. Deliverables
Code: Python notebooks and scripts for ML models, Flask backend APIs

Deployment:
Streamlit dashboard for admin
Mobile-first frontend using Flutter or React Native

Report:
Documentation of system architecture, testing logs, ethical risks and mitigation
GitHub README with user guide

6. Ethical & Sustainability Checks
Bias Mitigation: Ensure model fairness by testing across regional farmer contributions and product variants

Environmental Impact: Deploy lightweight models to optimize power consumption on rural smartphones

Scalability: Ensure offline-first functionality (data caching) and minimal bandwidth usage

7. Sample Project Outline
Phase	Tasks
Ideation	Identify user pain points via surveys; validate AI feasibility
Development	Build forecasting model; set up backend; build frontend UI/UX
Testing	Run A/B tests on model accuracy; test mobile ordering system
Deployment	Deploy on mobile; release beta version; conduct user training
Monitoring	Collect feedback; track order volumes, spoilage reduction, user growth

8. How AI for Software Engineering Concepts Apply
Key Concept	Application
Automated Testing	Ensures freshness predictions are reliable
CI/CD Pipelines	Allows frequent feature releases for customers and farmers
Version Control (Git)	Enables collaboration with agri-tech developers and open-source contributors
Ethical AI Design	Prevents exclusion of low-literacy users or small-scale vendors
Modular Code	Reusable components for payments, SMS alerts, or vendor onboarding

🌱 Reflection Questions
SDG Alignment: Helps reduce food waste (SDG 2) and increases farmer profitability through AI-powered insights (SDG 8).

Ethical Risks: Risk of excluding digitally illiterate vendors—addressed via USSD/SMS integration and audio guides.

Software Sustainability: Clear documentation, modular functions, continuous testing, and open-source access.

Impact: Improved income for small dairy vendors, reduced spoilage rates, higher consumer access to nutritious Mursik.

# Tecmos Mursik Palace App (AI-Driven Platform)
# Streamlit Prototype for Web Dashboard (Admin & Vendor View)

import streamlit as st
import pandas as pd
import numpy as np
from datetime import datetime, timedelta
import random

# -------------------- Title and Sidebar --------------------
st.set_page_config(page_title="Tecmos Mursik Palace", layout="wide")
st.sidebar.title("Tecmos Mursik Palace")

# Navigation
page = st.sidebar.radio("Navigate", ["Dashboard", "Forecast Demand", "Spoilage Risk Alerts", "Vendor Uploads", "About"])

# -------------------- Sample Dataset --------------------
@st.cache_data
def generate_sample_data():
    dates = pd.date_range(start=datetime.today() - timedelta(days=30), periods=30)
    sales = np.random.randint(10, 100, size=30)
    spoilage = np.random.randint(0, 5, size=30)
    return pd.DataFrame({"Date": dates, "Sales": sales, "Spoilage": spoilage})

data = generate_sample_data()

# -------------------- Pages --------------------
if page == "Dashboard":
    st.title("📊 Sales & Spoilage Dashboard")
    col1, col2 = st.columns(2)

    with col1:
        st.metric("Total Sales (Last 30 days)", f"{data['Sales'].sum()} Litres")
    with col2:
        st.metric("Total Spoilage", f"{data['Spoilage'].sum()} Litres")

    st.bar_chart(data.set_index("Date")[["Sales", "Spoilage"]])

elif page == "Forecast Demand":
    st.title("📈 Demand Forecast (AI Model Stub)")
    future_dates = pd.date_range(start=datetime.today(), periods=7)
    predicted_sales = [random.randint(60, 90) for _ in range(7)]
    forecast_df = pd.DataFrame({"Date": future_dates, "Predicted Sales": predicted_sales})
    st.line_chart(forecast_df.set_index("Date"))
    st.success("Forecasts generated using placeholder AI model.")

elif page == "Spoilage Risk Alerts":
    st.title("🚨 Spoilage Risk Prediction")
    spoilage_risks = [random.random() for _ in range(10)]
    vendors = [f"Vendor_{i}" for i in range(1, 11)]
    risk_df = pd.DataFrame({"Vendor": vendors, "Risk Score": spoilage_risks})
    high_risk = risk_df[risk_df["Risk Score"] > 0.7]
    st.table(high_risk)
    if not high_risk.empty:
        st.warning("Contact vendors above to take preventive measures.")

elif page == "Vendor Uploads":
    st.title("📤 Vendor Product Submission")
    vendor_name = st.text_input("Vendor Name")
    litres = st.number_input("Litres Produced", min_value=1, max_value=500)
    upload_time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    if st.button("Submit Entry"):
        st.success(f"Upload received from {vendor_name} at {upload_time} for {litres} litres.")
        st.info("Note: This is a stub. Backend storage/database not connected.")

elif page == "About":
    st.title("ℹ️ About Tecmos Mursik Palace")
    st.markdown("""
    **Tecmos Mursik Palace** is an AI-powered platform supporting sustainable traditional milk (mursik) supply in Kenya.

    **Features:**
    - AI-driven demand forecasts
    - Spoilage risk alerts
    - Vendor management dashboard
    - Promotes SDG 2 (Zero Hunger) & SDG 8 (Decent Work)

    _Built with Streamlit, Python & Love 🇰🇪._
    """)
