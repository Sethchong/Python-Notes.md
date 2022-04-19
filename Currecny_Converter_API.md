### Creating a simple currency converter
```python
date = input("Please enter the date (in the following format 'yyyy-mm-dd' or 'latest'): ")
base = input("Convert from: ")
currency = input("Convert to: ")
quantity = float(input("Enter the amount {}: ").format(base))

#Constructing the URL based on the user parameters and sendgin a request to the server 
url = base_url + "/" + date + "?base=" + base + "&symbols=" + currency
response = requests.get(url)

#Displaying the error message, if something went wrong 
if(response.ok is False):
	print("\nError {}:".format(response.status_code))
	# recall that response.status_code returns the status code
	print(response.json()['Error'])
else:
	data = response.json()
	# to directly convert the response to JSON format 
	rate = data['rates'][currency]
  # rates is something found inside the API content 
	result = quantity * rate 
	print("\n{0} {1} is equal to {2} {3}, based upon exchange rates on {4}".format(quantity,base,result,currency,data['data']))

```

