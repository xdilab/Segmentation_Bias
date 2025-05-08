# Seg_Bias
Project: Enhancing Fairness with Curriculum Learning
Overview
This project focuses on enhancing fairness in medical image segmentation while maintaining high accuracy. Specifically, we aim to create a model that performs well across diverse demographic groups, considering factors like race and gender. Our work leverages datasets from the OAI collection, which includes two primary datasets: one with hip radiographs and the other with knee radiographs.

The objective of this project was to develop a model that not only provides accurate segmentation results but also strives for fairness across various demographic groups. To achieve this, we explored several architectures and training strategies aimed at improving both fairness and performance.

Key Components
1. Model Architecture Selection
We employed multiple architectures to evaluate their performance in terms of both fairness (across demographic groups) and accuracy (measured by Intersection over Union, IoU). The architectures considered include:

U-Net

U-Net++

LinkNet

MANet

etc.

Based on our evaluations, we found that U-Net provided the best balance between accuracy and fairness, making it the base architecture for our subsequent experiments.

2. Training Strategies
After selecting U-Net, we experimented with various training strategies to enhance model fairness:

Random Shuffling: This is the baseline model, where the dataset is shuffled randomly without considering demographic attributes.

Random Interleaving by Race & Gender: In this strategy, the dataset is filtered by combining race and gender as an additional attribute for interleaving, aiming for better demographic fairness.

Diversity-Specific Models: For this approach, we trained separate models for each race and gender, targeting specific demographic groups individually.

3. Curriculum Learning Methods
We employed different curriculum learning strategies to improve training efficiency and fairness:

Self-Paced Learning (SPL): Starting from the second epoch, the data loader is sorted based on the IoU scores of the samples, moving from the easiest samples to the hardest.

Balanced Curriculum Learning (BCL): Similar to SPL but with an incremental data strategy. Initially, only a portion of the data is used, and by each epoch, more difficult samples are introduced.

Teacher-Student Learning: This method requires a pre-trained model (teacher) to guide a student model. The student learns by minimizing the IoU differences between its predictions and those of the teacher. Data loading is sorted in a similar way to SPL but focusing on minimizing the difference between the teacher and student models.

4. Fairness Metric
To assess the fairness of our models, we used the Swed Error Ratio (SER) as a key metric. SER measures the fairness of the model across different demographic groups, where a lower SER indicates better fairness. SER is calculated as follows:


SER(G)= Min(1−IoUG)/Max(1−IoUG)
​
 
Where 
G represents a specific demographic group (e.g., race or gender). Our goal was to minimize the SER values, indicating that the model performs equally well across all demographic groups.

5. Custom Loss Function
To improve the performance of the models, we introduced a Tied Progressive Loss function. This custom loss proved to be more effective than traditional loss functions, providing better results in both accuracy and fairness across the models.

Application
These methods were applied to both hip radiographs and knee radiographs from the OAI dataset. The goal was to ensure that the resulting segmentation models performed well across all demographic groups, addressing the common biases present in many machine learning models.

Results
Fairness: The various curriculum learning strategies and model architectures significantly improved the model's fairness across different demographic groups, as measured by the Swed Error Ratio (SER).

Accuracy: The U-Net architecture, combined with curriculum learning methods and the custom loss function, achieved a robust balance between accuracy (IoU) and fairness.

For more information, please visit the upcoming paper: Coming Soon
