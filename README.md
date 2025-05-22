# TECHIN515 Lab 4 Magic Wand - Discussion Questions

   - Data collection process and results
   - Edge Impulse model architecture and optimization
   - Performance analysis and metrics

<img width="537" alt="Screenshot 2025-05-22 at 12 09 11 PM" src="https://github.com/user-attachments/assets/2e36ab0d-98d2-43f3-b147-3264294d92cf" />
<img width="547" alt="Screenshot 2025-05-22 at 12 09 24 PM" src="https://github.com/user-attachments/assets/8ca803d3-d88f-46ff-8e8b-3652831417e1" />
<img width="1253" alt="Screenshot 2025-05-22 at 11 25 31 AM" src="https://github.com/user-attachments/assets/ed08e459-63b0-48c1-9f29-fc548d2f336e" />
<img width="776" alt="Screenshot 2025-05-22 at 11 50 54 AM" src="https://github.com/use[kellypeng-project-1 - Spectral features - Edge Impulse.pdf](https://github.com/user-attachments/files/20399024/kellypeng-project-1.-.Spectral.features.-.Edge.Impulse.pdf)
[sgks.pdf](https://github.com/user-attachments/files/20399023/sgks.pdf)
[kellypeng-project-1 - Classifier - Edge Impulse.pdf](https://github.com/user-attachments/files/20399022/kellypeng-project-1.-.Classifier.-.Edge.Impulse.pdf)
r-attachments/assets/60141a03-a3ba-4ccd-9c3d-466346f6460d" />


## Part 1: Data Collection Discussion

https://github.com/user-attachments/assets/294a693b-21ff-4620-a7a0-050fe3f3c37a


**Question:** Why should you use training data collected by multiple students rather than using your own collected data only? Think about the effectiveness and reliability of your wand.

**Answer:** Using training data collected by multiple students rather than relying solely on individual data is crucial for creating an effective and reliable magic wand system. When only one person's gesture data is used for training, the model becomes highly specialized to that individual's specific movement patterns, hand size, gesture speed, and execution style, leading to severe overfitting. This results in a model that performs well for the original data collector but fails dramatically when used by others. In contrast, incorporating data from multiple students introduces natural variation in gesture execution, accounting for differences in physical characteristics, movement habits, and interpretation of the same gesture. This diversity helps the model learn the essential features that define each gesture while remaining robust to individual differences. The increased dataset size from multiple contributors also provides better statistical representation of each gesture class, reducing the likelihood of the model memorizing specific patterns rather than learning generalizable features. Furthermore, real-world applications demand that the magic wand work reliably across different users, making multi-user training data essential for practical deployment. The collaborative approach also helps identify and address edge cases or unusual gesture variations that might not appear in a single person's data, ultimately creating a more robust and universally applicable gesture recognition system.

## Part 2: Model Development Discussions

### Window Size Effect Analysis

**Discussion:** The effect of window size on gesture recognition involves several interconnected factors that significantly impact model performance and computational requirements. Regarding the number of samples generated, larger window sizes capture more data points per gesture instance, which increases the richness of each training sample but also means fewer total gesture samples can be extracted from the same amount of raw data. This trade-off affects the model's ability to learn from diverse examples versus learning detailed patterns from individual gestures. The window size directly determines the input layer architecture of the neural network, since each sample requires input neurons equal to the number of sensor channels multiplied by the window length. For accelerometer data with three axes, a one-second window at 100Hz sampling rate would require 300 input neurons, while a two-second window would need 600 neurons. This scaling dramatically increases computational complexity, memory requirements, and the risk of overfitting, especially with limited training data. When considering effectiveness for capturing slow-changing patterns, larger windows provide crucial temporal context that allows the model to understand complete gesture sequences, particularly important for complex movements that unfold over extended periods. However, excessively large windows may dilute important gesture features with irrelevant background movement or transitions between gestures. The optimal window size must balance capturing sufficient temporal information to characterize complete gestures while maintaining computational efficiency and avoiding the inclusion of irrelevant data that could confuse the classifier.

### Processing and Learning Block Selection

**Processing Block Justification:** For this gesture recognition application, the Spectral Features processing block represents the most appropriate choice due to its ability to capture frequency domain characteristics that distinguish different movement patterns. Human gestures often exhibit distinct frequency signatures based on their speed, rhythm, and execution style, making spectral analysis particularly effective for classification. The spectral features can identify whether a gesture involves rapid movements, smooth transitions, or specific oscillatory patterns that characterize different spells. Alternative processing blocks like Raw Data preserve all temporal information but may introduce unnecessary noise and computational overhead, while other specialized blocks might not capture the essential characteristics of gesture patterns as effectively as frequency domain analysis.

**Learning Block Justification:** The Classification (Keras) learning block provides the optimal framework for this multi-class gesture recognition problem due to its flexibility and proven effectiveness in similar applications. This block allows for customization of neural network architecture, including the number of hidden layers, activation functions, and optimization algorithms, enabling fine-tuning for the specific characteristics of gesture data. The Keras implementation supports various regularization techniques essential for preventing overfitting in sensor data applications, and its integration with Edge Impulse ensures efficient deployment to resource-constrained embedded systems. Unlike simpler classification methods, the neural network approach can learn complex non-linear relationships between input features and gesture classes, which is crucial given the subtle differences that may distinguish similar gestures.

### Feature Quality Assessment and Decision Boundaries

Generated features demonstrate quality when they exhibit clear separation between different gesture classes in the feature space, with minimal overlap regions that could cause misclassification. High-quality features should show distinct clustering patterns where samples from the same gesture type group together while maintaining significant distance from other gesture clusters. The decision boundary analysis reveals natural separation lines that can effectively discriminate between classes, typically appearing as regions of lower data density between clusters. When sketching decision boundaries, the optimal approach involves identifying linear or non-linear separations that maximize the margin between different gesture classes while minimizing the number of misclassified training samples. The effectiveness of these boundaries can be visualized by observing how well they separate the feature clusters and by analyzing the confidence regions around each class boundary, with good features showing wide, clear separation zones that suggest robust classification performance.

### Model Performance Enhancement Strategies

**Strategy 1: Data Augmentation and Synthetic Data Generation** represents a powerful approach to improving model robustness by artificially expanding the training dataset through controlled modifications of existing samples. This involves adding realistic noise to sensor readings to simulate real-world conditions, applying temporal scaling to account for variations in gesture execution speed, and introducing slight rotational transformations to account for different sensor orientations during use. The augmentation process can also include amplitude scaling to simulate different gesture intensities and temporal shifting to capture variations in gesture timing. These modifications help the model generalize better to unseen variations in gesture execution while maintaining the essential characteristics that define each gesture class.

**Strategy 2: Ensemble Methods and Model Combination** offers another significant avenue for performance improvement by leveraging the strengths of multiple complementary models. This approach involves training several models with different architectures, hyperparameters, or feature representations, then combining their predictions through voting schemes or weighted averaging based on individual model confidence scores. The ensemble approach reduces the impact of individual model biases and provides more robust predictions, especially for ambiguous gesture samples that fall near decision boundaries. Implementation can include training models with different window sizes to capture both fine-grained and broad temporal patterns, or using different processing blocks to capture complementary aspects of the gesture data, ultimately creating a more comprehensive and reliable classification system.
```

1. Code and Documentation:
   - All sketches with comments
   - Python scripts for data collection
   - Your dataset
   - Edge Impulse project export
   - README with setup instructions

2. Report (PDF format) including:
   - Pictures of hardware setup and connections
   - Data collection process and results
   - Edge Impulse model architecture and optimization
   - Performance analysis and metrics
   - Answers to questions and your choices to all design options with justifications
   - Demo video link
   - Challenges faced and solutions

3. Demo Video (less than 3 minutes):
   - Show hardware setup
   - Demonstrate data collection
   - Show real-time gesture recognition
   - Include performance metrics

4. Enclosure and Battery are due on **May 20th, 2025**.
   - Components including board, MCU, IMU sensor, and wiring should be fully enclosed.
   - Use mounting holes to stablize the board within your wand.
   - Use reasonable enclosure based on your background in TECHIN511. For example, a box or staff is considered and **inappropriate enclosure** for the wand.
  
## Troubleshooting

- **Port not found**: Specify the port manually with `--port COM3` (Windows) or `--port /dev/ttyUSB0` (Linux/Mac)
- **Permission denied**: On Linux/Mac, run `sudo chmod 666 /dev/ttyUSB0` (replace with your port)
- **No data received**: Check connections and ensure the sketch is uploaded correctly
