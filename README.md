# Grounded Naming Game with Visual Perception (CNN + Multi-Agent Simulation)

## Project Overview
This project implements a **Grounded Naming Game** in which a population of agents develops a shared vocabulary to name perceived entities.
Unlike classical naming games, communication is **grounded in visual perception**, using a convolutional neural network (CNN) trained on real-world images.

The experiment investigates how perceptual accuracy influences the emergence of shared linguistic conventions.

---

## Dataset
The visual input is based on the **Animals-10** dataset from Kaggle:
https://www.kaggle.com/datasets/alessiocorrado99/animals10

- ~28,000 RGB images
- 10 animal classes: dog, cat, horse, spider, butterfly, chicken, sheep, cow, squirrel, elephant
- Images sourced from Google Images
- Significant class imbalance in the original dataset

### Dataset Preprocessing
To improve data quality and efficiency:
- Low-quality and unclear images were removed
- A balanced subset was created across classes
- Only part of the dataset was used to reduce computational cost
- The dataset was split into:
  - training and test sets
  - pre-linguistic and linguistic subsets
- A balanced sampler ensured equal class representation per batch
- Data was loaded using PyTorch DataLoaders and converted to tensors only once to save memory

---

## Neural Network Architecture
Each agent is equipped with a perceptual system called **DescribeNetAnimals**, a CNN used to recognize animal categories.

### Architecture Details
- Input: 128×128 RGB images
- Four convolutional blocks, each including:
  - Convolution layers
  - Batch normalization
  - ReLU activation
  - Max pooling
- Fully connected hidden layer
- Output layer with 10 units (one per animal class)
- Loss function: Cross-entropy
- Optimizer: Adam

The CNN acts as a **perception module**, transforming visual input into internal representations that can be associated with symbolic names during communication.

---

## Training Setup (Pre-linguistic Phase)
Before communication starts, agents learn to recognize visual categories.

Configuration:
- 5 agents
- 10 animal categories
- 10 training epochs per agent
- Accuracy and loss tracked on training and validation sets

### Training Results
| Agent | Train Loss | Train Accuracy | Val Loss | Val Accuracy |
|------|------------|----------------|----------|--------------|
| 1 | 0.37 | 0.93 | 1.47 | 0.50 |
| 2 | 0.46 | 0.93 | 1.62 | 0.46 |
| 3 | 0.32 | 0.93 | 1.54 | 0.50 |
| 4 | 0.45 | 0.93 | 1.47 | 0.50 |
| 5 | 0.37 | 0.93 | 1.43 | 0.52 |

The agents learn the training data well, but validation performance is lower, indicating **overfitting**.
Nevertheless, validation accuracy remains well above chance level (0.10), providing sufficiently stable perceptual categories for communication.

---

## Grounded Naming Game Simulation
After the pre-linguistic phase, agents engage in a **Grounded Naming Game**:
- Each interaction presents 3 visual entities
- Agents attempt to communicate and agree on category names
- Vocabulary emerges through repeated interactions

### Simulation Results
- Communicative success stabilizes around **0.5**
- Conventionality also oscillates around **0.4–0.5**
- Construction inventory size grows rapidly, then stabilizes around **14–17 constructions**

The system develops partial coordination but does not converge to a fully stable shared lexicon.

Due to technical limitations of the FCG server, the simulation was limited to approximately **3,000 interactions**.
Longer simulations might lead to further stabilization.

---

## Key Insights
- Grounded communication can emerge even with imperfect perception
- Limited classification accuracy (~50%) constrains communicative success
- Perceptual quality strongly affects linguistic convergence
- Better visual models would likely lead to more stable shared vocabularies

---

## Future Improvements
- Use a deeper CNN architecture
- Apply data augmentation
- Increase training data
- Run longer simulations
- Explore transfer learning for perception

---

## Technologies Used
- Python
- PyTorch
- Convolutional Neural Networks
- Multi-Agent Simulation
- Grounded Naming Game framework
