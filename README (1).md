Multimodal House Price Prediction Using Satellite Imagery

This project aims to predict residential house prices by combining structured tabular housing data with satellite imagery using a multimodal machine learning approach. Traditional house price prediction models rely primarily on numerical attributes such as area, number of bedrooms, and year of construction. While these features are informative, they do not fully capture the surrounding environment and neighborhood characteristics that significantly influence property value. To address this limitation, this project integrates satellite images to provide visual context alongside tabular features.

The dataset consists of house-level attributes including structural, geographic, and historical information. In addition to this tabular data, satellite images corresponding to each house location are collected using the Mapbox Static Satellite Images API. Each image captures neighborhood-level details such as road connectivity, greenery, building density, and nearby infrastructure. These visual cues complement the numerical data and enhance the predictive capability of the model.

The workflow begins with satellite image collection, where each house’s latitude and longitude are used to download a fixed-size satellite image. These images are stored locally and linked to the dataset through an image path column. To ensure data quality, preprocessing steps are applied to clean missing values, remove irrelevant features, and normalize numerical inputs. Geographic coordinates are validated to ensure accurate image-to-house mapping.

Baseline models are first trained using only tabular data to establish reference performance. Multiple regression models, including Linear Regression, Ridge Regression, Lasso Regression, Random Forest, and XGBoost, are evaluated using RMSE and R² score. This baseline analysis provides insight into how well numerical features alone can predict house prices.

To incorporate visual information, satellite images are processed using a pretrained convolutional neural network. A ResNet50 model, trained on ImageNet, is used as a feature extractor. Each satellite image is passed through the network to obtain a 2048-dimensional feature vector representing high-level visual patterns. Since this process is computationally expensive and can take several hours, extracted image features are saved to disk as NumPy files. The notebook is designed with a control flag that allows loading precomputed features instead of re-running the extraction, ensuring reproducibility and efficient execution.

Once both tabular and image features are available, they are combined into a single fused feature representation. This multimodal feature set enables the model to learn relationships that span both numerical and visual domains. Advanced regression models are then trained on this fused dataset. Among the evaluated models, XGBoost demonstrates the best performance in terms of validation error and explanatory power, making it the final selected model.

The final stage of the project involves generating predictions for the test dataset. The trained multimodal XGBoost model is used to predict house prices, and the results are exported as a plain CSV file. The submission file follows the required format with house identifiers and predicted prices and is generated programmatically to ensure compatibility with automated evaluation systems.

Overall, this project demonstrates that incorporating satellite imagery into house price prediction models provides meaningful performance gains over traditional tabular-only approaches. It highlights the importance of neighborhood context and showcases the effectiveness of combining computer vision techniques with structured data for real-world prediction tasks.

About the files i have attached in short 

DATA_FETCHER.ipynb downloads satellite images for each house location using latitude and longitude coordinates via the Mapbox Static Images API and stores them locally.

01_preprocessing (2) (1).ipynb performs data cleaning and preprocessing, including handling missing values, removing irrelevant features, and preparing tabular data for modeling.

02_Model_Training_Baseline (2).ipynb trains and evaluates baseline regression models using only tabular features to establish reference performance metrics.

04_Image_Feature_Extraction.ipynb extracts visual features from satellite images using a pretrained ResNet50 model. Precomputed features are loaded by default to avoid re-running expensive computations.

Prediction file download.ipynb generates final predictions on the test dataset using the trained multimodal model and exports the results as a CSV file.

23113075.csv contains the final predicted house prices in the required submission format.

Enrollment Number: 23113075

Project Domain: Multimodal Machine Learning (Computer Vision and Tabular Data)

