

### <u>Architecture</u>
![[Pasted image 20251125120206.png|300]]
#### Input Nodes
- The input layer receives the raw data that the network will learn from. Each node in this layer, labeled from x₁ to xn, represents a single feature or attribute of the input data. For example, in an image recognition task, these could be the pixel values of an image.
- The input nodes themselves, such as x₁ and x₂, do not perform any computation. They simply pass the input values to the next layer. The arrows originating from these nodes indicate the direction of information flow, which is strictly forward in this type of network.
- **Traditional AI Example:** If we are analyzing a house, the inputs might be `Square Footage (2000)`, `Number of Bedrooms (3)`, and `Zip Code`
- **Generative AI Example:** If we are reading a sentence, the computer converts words into a long list of numbers (vectors) representing meaning.
#### Hidden Nodes
- The hidden layers are where the majority of the computation occurs. Each node in the hidden layer receives inputs from all the nodes in the previous layer.
- These layers are made of thousands (or billions) of **Artificial Neurons**. Each single neuron acts as a "mini-decision maker"; it receives data, processes it, and decides whether to pass it on.
- **Weights (The Importance Sliders):** Every connection between neurons has a "Weight." This is a number that determines how important that specific input is.
- **Biases (The Threshold):** A "Bias" is an extra number added to the total. It acts like a tipping point.
	- _Analogy:_ Imagine you are deciding where to eat lunch. Distance might have a high weight (very important to you). Decor might have a low weight (you don't care much). Even if the restaurant is close (high weight on distance), if it's not open (bias), you won't go.
- **The Activation Function (The "Switch")** Once the neuron adds up all its inputs (multiplied by their weights) and adds the bias, it passes the result through an **Activation Function**. This turns the math into a simple output, often strictly between 0 and 1. Much like a light switch: if the signal is strong enough, the neuron turns "ON" and passes the signal to the next layer.
- _In the AI:_ It shifts the activation so the neuron only "fires" when a certain condition is met.
- The nodes in the hidden layer, labeled from h(1)₁ to h(1)m, compute a weighted sum of their inputs and then apply a non-linear activation function to this sum. This non-linearity is crucial, as it allows the network to learn complex patterns and relationships within the data. The superscript (1) indicates that this is the first hidden layer; a deep neural network would have multiple such layers.
#### Output Nodes
- Finally, the information flows to the output layer, shown in red. This layer produces the final result of the network's computation. The number of nodes in this layer depends on the specific task; for example, in a classification problem with 'k' classes, there would be 'k' output nodes, each representing the probability of the input belonging to a particular class.
- The output nodes, labeled from y₁ to yk, also receive inputs from the previous layer and perform a computation. The output of these nodes represents the network's prediction or decision. For instance, in a regression problem, a single output node might predict a continuous value.

The lines connecting the nodes between layers represent the weights of the neural network. These weights are the parameters that the network learns during the training process. Each connection has an associated weight that scales the signal passing through it, effectively determining the influence of one neuron on another.

- **Forward Pass:** The model makes a guess based on current weights.
- **Loss Function 📉:** The system calculates the "Error" (difference between the Guess and the Actual Answer).
- **Optimizer (Gradient Descent) 📉:** The system calculates _how_ to adjust the weights to reduce that error.
- **Backpropagation 🔙:** The adjustments are sent backward through the network to update the weights.
- **Frozen Weights ❄️:** During use, the model stops learning. The weights are fixed.
- **New Input:** Unseen data is fed into the system.
- **Probabilistic Output:** The AI provides the most statistically likely answer (e.g., "75% chance this is a cat" or "The next most likely word is 'blue'").
- The AI is not "thinking" in real-time; it is retrieving complex mathematical patterns established during training.
### <u>Training Loop</u>
- How the AI moves from "guessing randomly" to "knowing." It’s a cycle that repeats millions of times.

**1. The Forward Pass (The Guess)**
- The AI takes an image (e.g., a Cat), runs the numbers through its current weights (which start out random), and makes a prediction.
- **Example:** It might say, "I am 60% sure this is a Toaster." (Obviously wrong, because it hasn't learned yet!)

**2. The Loss Function (The Scorecard 📉)**
- The system compares the AI's guess ("Toaster") with the actual correct answer label ("Cat").
- It calculates the difference mathematically. This difference is called the **Loss** or **Error**.
- **Goal:** We want this number to be as close to 0 as possible.

**3. The Optimizer & Backpropagation (The "Hot or Cold" Game 🔙)**
- The AI uses calculus to look at that Error and figure out _which_ specific weights contributed to the mistake.
- It sends a signal backward through the network: "Hey, the weight for 'Pointy Ears' was too low! Increase it! The weight for 'Metallic Sheen' was too high! Decrease it!"
- **Analogy:** Imagine playing "Hot or Cold" to find a hidden object.
    - **Loss:** Being told "You're freezing!"
    - **Optimizer:** Deciding to take a big step in the opposite direction.

**4. The Update**
- The weights are nudged slightly in the right direction. The next time the AI sees a cat, it might be "55% Toaster, 5% Cat." Still wrong, but _less_ wrong.

### <u>Inference / Application</u>

**1. Frozen Weights (The "Done" State ❄️)**.
- Unlike in training, the feedback loop is cut. The weights do **not** change when you use ChatGPT or a spam filter.
- **Key Concept:** If the AI makes a mistake here, it doesn't learn from it immediately. It will keep making that mistake until engineers retrain it with a new version.

**2. The Forward Pass (Again)**.
- New, unseen data enters the system. The math is calculated using the weights established during training.

**3. The Output: Traditional vs. Generative**. Here is how the output differs:
- **Traditional AI (Discriminative):**
    - **Job:** Categorize or Predict a Value.
    - **Process:** The final layer is a list of categories (e.g., "Cat," "Dog," "Toaster").
    - **Output:** The category with the highest score wins.
    - _Example:_ "This email is 99.8% Spam."
- **Generative AI (LLMs, Image Generators):**
    - **Job:** Create the "next piece" of data.
    - **Process:** The AI isn't picking a category; it's predicting the **next token** (word, pixel, or sound) in a sequence.
    - **Output:** It generates a probability list for every possible next word in the dictionary. It then picks one (usually the most likely) and feeds it back into itself to predict the _next_ word.
    - _Example:_ Input: "The sky is..." -> Prediction: "blue (80%), cloudy (10%), falling (1%)."

---

