import streamlit as st
import pandas as pd

# Sample onboarding data
onboarding_data = {
    "Week 1": ["Introduction to the team", "Company overview", "Access to tools and resources", "Initial 1-on-1 session"],
    "Week 2": ["Product training", "Work on mock projects", "Attend team meetings", "Progress review"],
    "Week 3": ["Financial and project management overview", "Customer service excellence training", "Feedback session"],
    "Week 4": ["Hands-on project work", "Mentorship session", "Go-live preparation", "Final feedback and assessment"]
}

# Track completion and feedback
if "completed_tasks" not in st.session_state:
    st.session_state.completed_tasks = {week: [False]*len(tasks) for week, tasks in onboarding_data.items()}

if "feedback" not in st.session_state:
    st.session_state.feedback = {week: [""]*len(tasks) for week, tasks in onboarding_data.items()}

st.title("30-Day Onboarding Plan")

# User details
name = st.text_input("Enter your name")
email = st.text_input("Enter your email")
employee_code = st.text_input("Enter your employee code")

st.header("Week-wise Onboarding Plan")

# Display onboarding plan week by week
for week, tasks in onboarding_data.items():
    st.subheader(week)
    for i, task in enumerate(tasks):
        # Checkbox for marking tasks as complete
        completed = st.checkbox(f"{task}", value=st.session_state.completed_tasks[week][i])
        st.session_state.completed_tasks[week][i] = completed

        # Text area for feedback
        feedback = st.text_area(f"Feedback for {task}:", value=st.session_state.feedback[week][i])
        st.session_state.feedback[week][i] = feedback

# Option to download progress report
def download_report():
    report_data = {
        "Week": [],
        "Task": [],
        "Completed": [],
        "Feedback": []
    }
    for week, tasks in onboarding_data.items():
        for i, task in enumerate(tasks):
            report_data["Week"].append(week)
            report_data["Task"].append(task)
            report_data["Completed"].append(st.session_state.completed_tasks[week][i])
            report_data["Feedback"].append(st.session_state.feedback[week][i])

    df = pd.DataFrame(report_data)
    return df.to_csv(index=False).encode('utf-8')

st.download_button("Download Onboarding Report", data=download_report(), file_name="onboarding_report.csv")

# Feedback and completion status
st.success("Your onboarding tasks and feedback have been saved!")
