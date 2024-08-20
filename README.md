# -DLASU24-mission-Jana-Aly-Eldin-Elsayed-
## Model 1: Simple DNN Model

**Assumptions**
- **Hidden Size**: I assumed a hidden size of 64 neurons for each layer, expecting it to provide a balance between model complexity and generalization.
- **Batch Size**: A batch size of 32 was chosen as a standard starting point, allowing for relatively stable updates while being computationally manageable.
- **Learning Rate**: The learning rate was set to 0.001, which is a common starting point, aiming for a balance between learning speed and stability.

**Loss Function**
- **MSELoss()**: Used as the loss function since the task was a regression problem. MSELoss is straightforward and commonly used for such tasks.

**Insights**
- The model’s performance, as indicated by the loss, was highly erratic across epochs. This fluctuation suggested that the model might be struggling to learn consistently from the data.

**Conclusions**
- **Model Instability**: The instability in the loss indicates potential issues with the model architecture, learning rate, or data preprocessing. The DNN may not have been complex enough to capture the underlying patterns, or the learning rate might have been too high, causing the model to oscillate during training.

**Bottlenecks**
- **Difficulty in Assessment**: Due to the fluctuating loss values, it was challenging to determine whether the model was actually improving. This made it hard to decide on the next steps, such as adjusting hyperparameters or moving on to a more complex model.

## Model 2: Convolutional Neural Network (CNN)

**Assumptions**
- **Data Adjustment**: The provided data was in 2D, but the convolutional layers required 4D input. The input data was adjusted accordingly before being fed into the network.
- **Hyperparameters**: Hyperparameters were determined through trial and error until the training loop successfully ran.
- **Batch Size**: Maintained at 32, consistent with the previous model.

**Loss Function**
- **MSELoss()**: Continued using MSELoss() as it is appropriate for regression tasks.

**Insights**
- **Training Time**: The model took a long time to train, which was likely due to the initial architecture consisting of three convolutional layers and three fully connected layers.

**Conclusions**
- **Model Architecture**: Reduced the number of convolutional layers from three to two while keeping three fully connected layers to improve training efficiency.
- **Working Model**: The effective model is `CNN1()`; the first model did not perform as expected.

**Bottlenecks**
- **Difficulty in Finding Optimal Configuration**: Finding the right hyperparameters and model configuration was challenging. Adjustments were necessary to balance training time and model performance.


## Model 3: CNN Convolving Through Time

**Description:**  
The third model is a CNN designed to convolve through time, utilizing a time window parameter of 5. To accommodate the sequential nature of the data, the position of the features and time steps was adjusted, and Conv1D was used instead of Conv2D. The previous 2D architecture resulted in errors, but using Conv1D resolved these issues and allowed the model to function correctly.

**Architecture:**
- **Time Window Parameter:** 5
- **Convolutional Layers:** 2
- **Fully Connected Layers:** 2
- **Batch Size:** 32
- **Loss Function:** `MSELoss()`

**Enhancements:**
To improve learning, a weight decay parameter was added to the optimizer function. This adjustment enhances model performance and regularization.

**Performance:**
This model showed improved performance over the previous two models. The training loss consistently decreased with each epoch, reflecting better learning from the sequential data.

**Summary:**
The CNN model with time convolution performed better due to its effective handling of sequential data. Switching to 'Conv1D' and adjusting the position of features and time steps were crucial changes that allowed the model to work effectively. The use of weight decay further contributed to its enhanced learning capabilities.

## Model 4: RNN-Based Model

**Description:**  
The fourth model is an RNN-based architecture, which was found to be simpler in implementation compared to the CNN models. The RNN model has fewer complexities, such as the addition of the hidden state `hx` in the forward method.

**Architecture:**
- **RNN Layer:** 1
- **Fully Connected Layer:** 1
- **Hidden State `hx`:** Added to the forward method
- **Batch Size:** 32
- **Loss Function:** `MSELoss()`
- **Hyperparameters:** Same as previous models

**Enhancements:**
The model retained the same batch size and `MSELoss()` function as the CNN models, making it consistent with the earlier architectures. After evaluating the results and finding them satisfying, the architecture with one RNN layer and one fully connected layer was kept.

**Performance:**
The implementation of the RNN model was more straightforward, and it performed effectively with the same hyperparameters used in the CNN models.

**Summary:**
The RNN-based model provided a simpler implementation compared to the CNN models. With one RNN layer and one fully connected layer, the model delivered satisfying results, and this architecture was maintained. The addition of the hidden state `hx` in the forward method was a key difference, but overall, the model maintained consistency with previous hyperparameters and loss functions.

## Model 5: CNN-LSTM

**Description:**  
The fifth and final model is a CNN-LSTM architecture. I initially found it challenging to distinguish between RNN-LSTM and CNN-LSTM, but I implemented the LSTM using the RNN class. This was one of the fastest models I’ve run.

**Architecture:**
- **LSTM Layer:** 1
- **Fully Connected Layer:** 1
- **Hidden State `hx`:** Added to the forward method
- **Memory Parameter `c_x`:** Added to carry information across time steps, regulated by forget, input, and output gates
- **Batch Size:** 32
- **Loss Function:** `MSELoss()`
- **Hyperparameters:** Same as previous models

**Enhancements:**
In this model, alongside the hidden state parameter, there’s an additional `c_x` memory parameter, which acts as a conveyor belt, managing the flow of information through time steps.

**Performance:**
Despite initial concerns about RAM usage, the model trained faster than any other model when I switched to using a GPU and reduced the batch size from 64 to 32.

**Bottlenecks:**
The main challenge encountered with this model was the unexpected high RAM usage when running on a CPU. This issue was resolved by switching to a GPU and reducing the batch size from 64 to 32, which significantly improved training speed and efficiency.

**Summary:**
The CNN-LSTM model demonstrated impressive speed and efficiency. The addition of the `c_x` memory parameter enhanced its ability to manage temporal information. Running on a GPU with a reduced batch size led to optimal performance, making this the fastest model I’ve developed.


