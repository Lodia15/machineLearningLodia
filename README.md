
# სახლის ფასების პროგნოზირების პროექტი

## პროექტის მიმოხილვა
ეს მონაცემთა მეცნიერული პროექტი ეძღვნება საცხოვრებელი უძრავი ქონების ფასების პროგნოზირებას მანქანის სწავლების მეთოდების გამოყენებით. პროექტი აგებულია Kaggle-ის ცნობილ კონკურსზე "House Prices: Advanced Regression Techniques", რომელიც მონაწილეებს აფასებს სახლების ფასების პროგნოზირების ზუსტობის მიხედვით.

## კოდის სტრუქტურა
###### იმპლემენტაცია შედგება:

1.მონაცემთა გაწმენდა და პრეპროცესინგი

2.ფიჩერ ინჟინერია WOE ენკოდინგით

3.ფიჩერების შერჩევა RFE-ს გამოყენებით

4.მოდელების ტრენინგი და ევალუაცია

5.ექსპერიმენტების ტრეკინგი MLflow-ით


###  მონაცემთა წინასწარი დამუშავება

def clean_dataset(raw_data: pd.DataFrame) -> pd.DataFrame:
    """
    ასუფთავებს მონაცემებს:
    - შლის სვეტებს, სადაც >80% მნიშვნელობები აკლია
    - ავსებს რიცხვით NaN-ებს 0-ით
    - ავსებს კატეგორიულ NaN-ებს "UNKNOWN"-ით
    """
    

##  ფიჩერ ინჟინერია
WOE ენკოდინგი: მრავალმნიშვნელოვანი კატეგორიული ფიჩერებისთვის
One-Hot ენკოდინგი: ცოტა მნიშვნელობის მქონე კატეგორიული ფიჩერებისთვის

class CustomPreprocessor(BaseEstimator, TransformerMixin):
    def __init__(self, woe_columns, one_hot_columns):
        # ახორციელებს Weight of Evidence ენკოდინგს
        
        
###   ფიჩერების შერჩევა
რეკურსიული ფიჩერების ელიმინაცია (RFE) არჩევს 15 საუკეთესო ფიჩერს

კორელაციის ანალიზი შლის მაღალად კორელირებულ ფიჩერებს


###  მოდელების ტრენინგი
შეფასებული იქნა სამი მოდელი:
LinearRegression - 0.17
GradientBoostingRegressor - 0.15
RandomForestRegressor - 0.15

###  MLflow ტრეკინგი
ყველა ექსპერიმენტი ჩაიწერა DAGsHub-ზე:
https://dagshub.com/Lodia15/machineLearningLodia.mlflow/#/experiments/3?searchFilter=&orderByKey=attributes.start_time&orderByAsc=false&startTime=ALL&lifecycleFilter=Active&modelVersionFilter=All+Runs&datasetsFilter=W10%3D
