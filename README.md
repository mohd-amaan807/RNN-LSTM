✍️ Character-Level Text Generation (Simple RNN vs. LSTM Simulation)
This project is a character-level text generation model implemented in a Python Jupyter notebook (RNN_LSTM.ipynb).
It uses a simple transition probability model derived from a small corpus to simulate the core differences between a Simple Recurrent Neural Network (RNN) and a Long Short-Term Memory (LSTM) network regarding their effective memory span.

The user interface is built using Gradio, allowing for easy experimentation directly within the notebook environment.

✨ Features
Character-Level Model: Builds a Markov-chain-like model based on single-character transitions from the provided corpus.

RNN Simulation: Simulates a Simple RNN's short-term memory by basing the next character prediction only on the last character generated (context_len=1).

LSTM Simulation: Simulates an LSTM's longer-term memory by looking for relevant context within a larger window of 10 characters (context_len=10).

Interactive Interface: A user-friendly Gradio interface for selecting the model type, providing seed text, and setting the generation length.

🛠️ Requirements
To run this notebook, you will need:

Python 3.x

Jupyter Notebook or Google Colab

The following Python libraries:

gradio

random

time (Standard Python library)

Installation
You can install the necessary dependencies using pip:

Bash

pip install gradio
🚀 How to Run
Clone the repository:

Bash

git clone [your-repo-link]
cd [your-repo-name]
Open the notebook: Open RNN_LSTM.ipynb using Jupyter Notebook, JupyterLab, or Google Colab.

Run all cells: Execute the code cells in the notebook. This will:

Load the corpus and build the transition probability model.

Start the Gradio interface.

Interact with the Interface:

A live Gradio application will appear directly below the code cell.

Select Model: Choose between Simple RNN and LSTM.

Seed Text: Enter the text you want the generation to start with (e.g., "The griffin").

Length: Set the number of characters to generate.

Click Generate Text to see the output.

🔬 Model Logic Explained
The generation logic is implemented in the generate_text function, which simulates the difference between the two model architectures:

1. Simple RNN Simulation
Python

if model_type == 'Simple RNN':
    # Simple RNN: Memory is short, only considers the last character.
    context_len = 1
    recent_context = context[-context_len:]
    last_char = recent_context[-1]
The "Simple RNN" mode uses a context length of 1. This means the model always predicts the next character based only on the immediately preceding character. This simulates the vanishing gradient problem, which typically limits Simple RNNs to very short-term dependencies.

2. LSTM Simulation
Python

else: # LSTM
    # LSTM: Simulates longer memory by looking for a valid context char
    # in a larger window.
    context_len = 10
    recent_context = context[-context_len:]
    # Find the most relevant character from the recent context that exists in our model
    last_char = next((char for char in reversed(recent_context) if char in transitions), context[-1])
The "LSTM" mode uses a larger context window of 10 characters. It scans this window for a relevant character to base the next prediction on.
This loosely simulates the gates and cell state mechanism of a real LSTM, which allows it to maintain and reference information from a much earlier point in the sequence, thus handling longer-range dependencies.

📚 Corpus
The model is trained on the following short, fantasy-themed corpus:

In the heart of a dense, ancient forest, where sunlight struggled to pierce the thick canopy, lived a creature of myth and legend. This was no ordinary beast, but a griffin, with the body of a lion and the head and wings of an eagle.
Its name was Ignis, and its feathers shimmered with the colors of a sunset. Ignis was a guardian, a protector of the forest's deepest secrets.
One of these secrets was the Moonpetal flower, a bloom that only opened under the light of a full moon and held the power to heal any ailment.
Many had sought the Moonpetal, but the forest's winding paths and the griffin's watchful eyes kept it safe. A young herbalist named Elara, however, was different. 
She came not with greed, but with a desperate plea. Her village was struck by a mysterious illness, and the Moonpetal was their only hope. She journeyed for days, her resolve unwavering.
When she finally reached the forest's heart, she did not draw a weapon. Instead, she offered a simple songbird's feather, a token of peace. Ignis, who had seen countless intruders, was intrigued. 
The griffin listened as Elara spoke of her village's plight. Moved by her sincerity, Ignis decided to trust her. The majestic creature led her to a hidden grove where the Moonpetals glowed with an ethereal light.
Elara took only a single bloom, thanking the griffin with a promise to protect the secret. She returned to her village, and the flower's magic worked. The illness vanished. The legend of the girl and the griffin became a whispered tale, a reminder that courage and compassion can be more powerful than any sword.
