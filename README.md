# Gesture_Recognition_CNN_TransferLearning
Problem Statement: 

•	We need to develop a cool feature in the smart-TV that can recognize five different gestures performed by the user which will help users control the TV without using a remote.
•	Each Video has 30 frames(images) in sequence for performing the gesture.
•	Each Video is tagged with a gesture name amongst the five gesture names. 
o Thumbs up: Increase the volume 
o Thumbs down: Decrease the volume 
o Left swipe: 'Jump' backwards 10 seconds 
o Right swipe: 'Jump' forward 10 seconds 
o Stop: Pause the movie 
•	The test set is withheld, but the final model`s performance will be tested on this.


Approach:

There are two types of architecture suggested for analyzing videos—

1.	3D Convolutional Network, or Conv3D- Just like in 2D conv, where we move the filter in two directions (x and y), in 3D conv, you move the filter in three directions (x, y and z).

2.	Convolutions + RNN-Here we can use LSTM or GRU and can also use Transfer learning. 

a.	To keep the model lightweight we prefer GRU over LSTM since it has less number of parameters. 
b.	We also made use of Mobilenet in transfer Learning because it is lightweight and suitable for Mobile based applications.

Preprocessing
1.	Cropping Images – We cropped the images to save compute and memory resources and making the images uniform. We got good results with (120,120) size images. It also removes the unnecessary background making training more efficient.
2.	Normalization- We also did normalizations to get rid of unnecessary noise and distortions.

Experiments
Experiment Number	Model	Result 	Decision + Explanation	Number of Parameters
1	Conv3D 1.15 frames to be sampled/video
2.Batch size of 32
3.Images cropped to 120,120
4.128 dense neurons in the two dense layers
5.Epoch of 20
6.Dropout of 0.25	Training Accuracy-0.97

Validation Accuracy-0.26

Early stopping at Epoch 11 as validation loss did not improve

Overfitting!	1.Increase number of frames/video and Epoch size to increase validation accuracy
2.Decrease the batch size so that model generalizes well and overfitting reduces	1155397
2	Conv3D 1.30 Epochs
2.Batch size of 20
3.20 frames to be sampled/video
4.Images cropped to 120,120
5.128 dense neurons in the two dense layers
6.Dropout of 0.25	Training Accuracy-0.96

Validation Accuracy-0.28

Early stopping at Epoch 11 as validation loss did not improve

Overfitting still!	1.Decrease the batch size further so that model generalizes well

2.Increase the dropout rate further to handle overfitting.	1155397
3	Conv3D    1.128 dense neurons in the two dense layers
2.Epochs = 30
3.Images cropped to 120,120
4.20 frames to be sampled\video
5.Batch size of 16
6.Dropout = 0.5	Training Accuracy-0.97

Validation Accuracy-0.94
(Epoch 27/30)
	1.Best model in Conv3D 
2.Val loss of 0.2 in Epoch 27
3.Overfitting completely handled and we got good and consistent result after Epoch 15, hence we would stop with this conv3D model and move to GRU and Transfer Learning.
4.GRU has less number of parameters than LSTM hence we prefer that.                           5.Since our model needs to be lightweight we prefer mobilenet for Transfer Learning.
6.This would be a probable candidate for our best model 
	1155397
4	CNN with GRU +Mobilenet         1.Mobilnet for Transfer Learning
2.128 GRU  cells
3.Images cropped to 120 ,120
4.20 frames\video to be sampled
5.Batch size of 8
6.Epoch of 25
7.Dropout of 0.5        	Training Accuracy-0.96

Validation Accuracy-0.81

Early stopping at Epoch 14 as validation loss did not improve
	1.Validation loss is high at 0.67 and also validation accuracy is not very good at 0.81
2.We will go with Mobilenet on all layers in next model for better learning.
3.Reduce the dropout to 0.25 for better learning of the model 	3693253
5	CNN with GRU+Mobilenet(all layers)
1.CNN with GRU and Mobilenet on all layers
2.128 GRU  cells.
3.Images cropped to 120 ,120
4.15 frames\video to be sampled.
5.Batch size of 8 
6.Epoch of 25.
7.Dropout of 0.25.	Training Accuracy-0.98

Validation Accuracy-0.95

(Epoch 22/25)
	1.Validation loss of 0.1171 in Epoch 22.
2.Best model so far in terms of accuracy	3693253
				
FINAL MODEL				
				
3	Conv3D    1.128 dense neurons in the two dense layers
2.Epochs = 30
3.Images cropped to 120,120
4.20 frames to be sampled\video
5.Batch size of 16
6.Dropout = 0.5	Training Accuracy-0.97

Validation Accuracy-0.94
(Epoch 27/30)
	1.Best model in Conv3D 
2.Val loss of 0.2 in Epoch 27
3.Overfitting completely handled and we got good and consistent result after Epoch 15, hence we would stop with this conv3D model and move to GRU and Transfer Learning.
4.GRU has less number of parameters than LSTM hence we prefer that.                         5.Since our model needs to be lightweight we prefer mobilenet for Transfer Learning.
6.This would be a probable candidate for our best model 
	1155397

Conclusion:
Finally we have to choose between two models which are best for Conv3D and CNN+GRU with mobilenet(marked in yellow in the above table) and select the best among Conv3D or CNN with GRU+ mobilenet. Let us also look at their Accuracy and loss graphs-
Model#3- Conv3D
 


Model#5-CNN with GRU+mobilenet
 
Let us compare both model side by side in the below table and make the final judgement-


Criteria	Model#3- Conv3D
	Model#5-CNN with GRU+mobilenet
	Winner
Number of parameters	1155397	3693253	Model#3 as Model#5 has more than 3 times more parameters.Model#3 wins by big margin
Model size on disk(.h5 model file)	13.3 Mb	42.4 Mb	Model#3 wins by big margin as it is less than 1/3rd of Model#5 size. An important consideration for Mobile App
Validation Loss	0.2	0.11	Model #5 wins by a small margin
Validation Accuracy	0.94	0.95	Model #5 wins by very narrow margin
Overfitting	As shown in graph, after Epoch#15 both loss and accuracy between training and validation set is almost similar   	As shown in the graph both loss and accuracy between training and validation set have differences between each other	Model#3 wins as there is hardly any overfitting
Consistency and stability	The graph for both loss and accuracy between training and validation sets are consistent i.e loss decreases and plateaus consistently whereas accuracy increases and plateaus at each epoch	There is hardly any consistency and there is lots of variation with each Epoch	Model#3 wins as it delivers consistent and predictable result whereas Model#5 lacks in consistency and stability
Simpler model	Model#3 is simpler comparatively	Model#5 is relatively complex with CNN+ GRU+ Transfer learning using mobilenet	Model#3 again wins for simplicity

We finally conclude than Model#3 which is Conv3D model is the final model we select for our application because our aim is to design the network such that it gives good accuracy on least number of parameters!!
