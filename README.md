# CS 4641 Project Team - Venomous Detection
## Project Proposal
Introduction & Problem Definition
The snake is a widely spread species across the world. Although many snake species do not possess fatal venom, several snake classes have poison in their venom that can impair human health severely. The symptoms include tissue death swelling, bleeding and destruction of blood cells, nerve damage and even death. According to a report, between 81,000-138,000 people die from snakebite each year. Many more survive but may do so with lasting disabilities or disfigurement. The staggering statistics of causality from snakebite makes it even more imperative to identify which snakes are harmless and which are venomous.

## Data Collection
The dataset is sourced from Kaggle. It contains 2044 snake images of size 400 * 400 with them labeled venomous or non-venomous. It includes a variety of snake species. We have around 87% trained data and 13% data for testing. 

## Methods/Process
The general approach of our project is supervised learning. Since the dataset we selected does not contain any numerical data, we will first preprocess the dataset and transfer the dataset into numerical value using the OrdinalEncoder in Python’s sklearn library. Then we will put the data into three models (Decision Tree, Random Forest, and Neural Network), and train the machine.
Potential Results & Discussion
Our goal is to take in snake images and detect which one is venomous. From this process, we hope to build a reliable model that hits 90% accuracy on telling users whether the snake is venomous and therefore preventing imprudent approaches. 

## Timeline and Expected Responsibilities


### Midterm Report (November 11)

Data pre-processing (due: Oct 14 AOE): Haosheng Wu 

Decision Tree model Implementation, Optimization, and Evaluation (due: Nov 4 AOE) : Mingxuan Nie, Dian Yang, Ruochen Shu

Page Report & Video (due: Nov 11 AOE) ：Jiaying Deng




### Final Project (December 6 )

Random Forest model Implementation, Optimization, and Evaluation (due: Nov 18 AOE): Mingxuan Nie, Dian Yang, Ruochen Shu, Haosheng Wu 

Neural Network model Implementation, Optimization, and Evaluation (due: Nove 25 AOE): Mingxuan Nie, Dian Yang, Ruochen Shu, Haosheng Wu

Page Report & Video (due: Dec 6 AOE): Jiaying Deng





### Reference:
_Osteroff, E. (n.d.). What happens when you’re bitten by a venomous snake? Www.nhm.ac.uk.https://www.nhm.ac.uk/discover/what-does-snake-venom-do-to-you.html_ 

_Rajabizadeh, M., & Rezghi, M. (2021). A comparative study on image-based snake identification using machine learning. Scientific reports, 11(1), 1-16._

_Amir, A., Zahri, N. A. H., Yaakob, N., & Ahmad, R. B. (2016, November). Image classification for snake species using machine learning techniques. In International Conference on Computational Intelligence in Information System (pp. 52-59). Springer, Cham._

