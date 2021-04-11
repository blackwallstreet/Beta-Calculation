
def start():
  x = input("Enter Stock Ticker:").upper()
  if x == 'EXIT':
    print('Program Ended')
  else:
    stock = yf.Ticker(x)
    SPX = yf.Ticker("SPY") # get historical market data
    stock = stock.history(start="2016-04-01",interval='1mo') #pulling historical stock data
    SPX = SPX.history(start="2016-04-01",interval='1mo') #retreiving historical SPX index data 

    SPX = SPX.dropna() #dropping columns with NA values
    stock = stock.dropna() #dropping columns with NA values 
    SPX = SPX[:-1] #removing the latest date 
    stock = stock[:-1] #removing the latest date
    stock['returns']= (stock.Close- stock.Close.shift(1))/stock.Close.shift(1) #Calulate montly returns for the stock
    SPX['returns'] = (SPX.Close- SPX.Close.shift(1))/SPX.Close.shift(1) #Calulat monthly returns for the SPX
    stock['index_returns']= SPX['returns'] #merge the index return values to the stock dataframe
    index_returns = stock.index_returns[1:] #create an array for the index removing the NA value
    stock_returns = stock.returns[1:] #create an array for stock returns remvoing the NA value 

    covariance = np.cov(stock_returns, index_returns) #Calculate covariance between stock and market
    beta = covariance[0,1]/covariance[1,1] #Calulate the beta 

    print(x,'Beta:', beta,'\n') #Print the returns
    start()



start()   
