import streamlit as st
import pandas as pd

# Configuração Visual Solar
st.set_page_config(page_title="RH Solar - Intercorrência", layout="wide")

st.markdown("""
    <style>
    .main { background-color: #FBF3F8; }
    h1 { color: #64003C; }
    .stButton>button { background-color: #E69600; color: white; border: none; }
    </style>
""", unsafe_allow_html=True)

st.title("☀️ Sistema de Gestão Solar - Intercorrência")

# Carregar os dados
@st.cache_data
def carregar_dados():
    # Substitua pelo caminho correto do seu arquivo CSV
    return pd.read_csv("Colaboradores ativos Intercorrência (1).xlsx - Ativos Intercorrência.csv")

df = carregar_dados()

# Abas de navegação
aba1, aba2, aba3 = st.tabs(["📋 Profissionais Ativos", "📅 Escala", "⚙️ Configuração"])

with aba1:
    st.header("Profissionais Ativos na Intercorrência")
    # Exibe a tabela editável
    df_editado = st.data_editor(df, use_container_width=True)

with aba2:
    st.header("Gestão de Escala")
    st.info("Aqui você verá o controle de faltas e trocas.")

with aba3:
    st.header("Entrada de Dados via WhatsApp")
    whatsapp_input = st.text_area("Cole a mensagem do WhatsApp aqui:")
    if st.button("Processar Mensagem"):
        st.write("Processando: ", whatsapp_input)

# Rodar com: streamlit run app.py
