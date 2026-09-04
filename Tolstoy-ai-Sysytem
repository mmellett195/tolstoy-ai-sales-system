import streamlit as st
from openai import OpenAI
import json

st.set_page_config(page_title="Tolstoy AI Sales Researcher")

st.title("Tolstoy AI Sales Researcher")
st.write("AI-assisted account research and sales planning")

account = st.text_input("Account Name")
website = st.text_input("Website")
discovery = st.text_area("Discovery Evidence (optional)")

if st.button("Research Account"):

    if not account:
        st.error("Enter an account name.")
        st.stop()

    client = OpenAI(api_key=st.secrets["OPENAI_API_KEY"])

    prompt = f"""
You are an AI sales research assistant for Tolstoy.

Research this account using public information only.

Account: {account}
Website: {website}
Discovery evidence: {discovery}

Never invent facts, performance numbers, stakeholders, technology usage,
or business problems.

Separate VERIFIED FACTS, ASSUMPTIONS, and UNKNOWNs.

Return:

1. Account score out of 100
2. Score rationale
3. Stakeholder hypothesis
4. Specific Tolstoy use case
5. Opening sales angle
6. Personalized outreach email
7. Key unknowns
8. Recommended next action
9. Opportunity/deal-plan update based on the discovery evidence

Use concise sales language.
"""

    response = client.responses.create(
        model="gpt-5.6-luna",
        tools=[{"type": "web_search"}],
        input=prompt
    )

    st.markdown(response.output_text)
