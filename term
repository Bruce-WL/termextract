import streamlit as st
import openai


# Change to your OpenAI API key
OPENAI_API_KEY = "your_OpenAI_API_key_here"
openai.api_key = OPENAI_API_KEY

# Set the page layout to wide
st.set_page_config(page_title="Extract Terms", page_icon=None, layout="wide")

# Title
st.title("Terminology Extraction")

source = "Welcomes the work of the Food and Agriculture Organization of the United Nations in developing guidance on the strategies and measures required for the creation of an enabling environment for small-scale fisheries, including the development of a code of conduct and guidelines for enhancing the contribution of small-scale fisheries to poverty alleviation and food security that include adequate provisions with regard to financial measures and capacity-building, including transfer of technology, and encourages studies for creating possible alternative livelihoods for coastal communities;"
target = "Salue le travail accompli par l'Organisation des Nations Unies pour l'alimentation et l'agriculture en ce qui concerne la définition d'orientations relatives aux stratégies et mesures nécessaires à la création de conditions propices aux petites pêches, notamment l'élaboration d'un code de conduite et de directives visant à accroître la contribution de la pêche à petite échelle à l'atténuation de la pauvreté et à la sécurité alimentaire et contenant des dispositions appropriées concernant l'aide financière et le renforcement des capacités, notamment le transfert de technologies, et souhaite que soient réalisées des études qui permettent de trouver de nouveaux moyens de subsistance pour les populations côtières ;"

# Form to add your items
with st.form("my_form"):
  # Get the user input
  source = st.text_area("Source", value=source, height=130, placeholder="Enter the source text...")
  target = st.text_area("Target", value=target, height=130, placeholder="Enter the target text...")
  number = st.number_input("Number of terms to extract", min_value=1, max_value=20, value=3)
  prompt = "Source: " + source + "\n" + \
           "Target: " + target + "\n\n" + \
           "Extract " + str(number) + " terms from the previous sentence pair. Type each source term followed by its target equivalent." + \
           " Display the results as a table; use language names as headers.\n\n|"

  def extract(prompt, max_tokens):
    response = openai.Completion.create(
    model="text-davinci-003",
    prompt=prompt,
    temperature=0.7,
    max_tokens=max_tokens,
    top_p=1,
    frequency_penalty=0,
    presence_penalty=0,
    n=1,
    )
    return response

  # Create a button
  submitted = st.form_submit_button("Extract terms")
  # If the button pressed, print the output
  if submitted:
    if len(source) > 0 and len(target) > 0:
      # Add loading animation
      with st.spinner("Extracting terms..."):
        max_tokens = 4000 - (len(prompt.split(" ")) * 5)
        response = extract(prompt, max_tokens)
        output = "|" + response.choices[0].text.strip()
        st.subheader("Terms extracted")
        st.markdown(output)
        print(output)
    else:
      st.write("Please enter both the source and target text.")


# Remove the menu
hide_streamlit_style = """
            <style>
            #MainMenu {visibility: hidden;}
            header {visibility: hidden;}
            footer {visibility: hidden;}
            </style>
            """
st.markdown(hide_streamlit_style, unsafe_allow_html=True)

# Remove whitespace from the top of the page and sidebar
st.markdown("""
        <style>
               .css-18e3th9 {
                    padding-top: 0rem;
                    padding-bottom: 10rem;
                    padding-left: 5rem;
                    padding-right: 5rem;
                }
               .css-1d391kg {
                    padding-top: 3.5rem;
                    padding-right: 1rem;
                    padding-bottom: 3.5rem;
                    padding-left: 1rem;
                }
        </style>
        """, unsafe_allow_html=True)
