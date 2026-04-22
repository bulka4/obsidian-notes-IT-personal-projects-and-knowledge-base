Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Unit and integration tests are functions testing our code, whether it works properly:
- Unit tests test small pieces of code
- Integration tests test big pieces of code, how small components interact with each other

For example, a unit test testing a function for creating new feature columns in a table can be:
```python
def test_feature_columns():
    df = pd.DataFrame({"age": [20]})
    result = create_features(df)
    
    assert "age_scaled" in result.columns
```

and integration test testing training a ML model can be:
```python
def test_full_pipeline():
    df = load_sample_data()
    features = create_features(df)
    model = train_model(features)
    
    assert model.predict(features).shape[0] == len(df)
```
