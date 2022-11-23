# Real Estate Scraper API Free Trial Guide

Use Real Estate Scraper API to extract publicly available property data from the most popular real estate websites without getting blocked.

In this tutorial, we’ll show you all the unique benefits and features you may want to explore to make the most out of your one-week free trial. We hope you’ll have a much clearer view of whether this solution is for you.

The primary focus of this tutorial is to walk you through a straightforward example of how to set up a Real Estate Scraper API from scratch. We highly recommend setting this up with a website of your choice as this would allow you to test out the quality of data gathered, ease of integration, and, most importantly, if this is a product that solves your needs and is worth investing time and money into. 

We’ll use Python with our Real Estate Scraper API in this example. If you wish to see more cases that use other languages and are more complex, please visit our [documentation](https://developers.oxylabs.io/scraper-apis/real-estate-scraper-api).

If you’ve found this tutorial before visiting our website, the easiest way to get a free trial is by visiting the [Real Estate Scraper API](https://oxylabs.io/products/scraper-api/real-estate) page and filling in the form.

<br>
<img src="/Real Estate Free Trial Form.png" width="400">

After filling in the form, you’ll receive an email with a username and password. You'll need these credentials to start using the Real Estate Scraper API.

<img src="/Real-Estate-Scraper-API-onboarding.png" width="400">

## How to set up a Real Estate Scraper API?

Let’s get into the concrete steps of integrating Real Estate Scraper API:

1. Open up your IDE (integrated development environment). 
2. Add the credentials you received on the email:

```python
import requests

username = 'username'
password = 'password'
```

3. Define the ‘source’ and paste the URL of the real estate website you want to scrape. In this example, we use [](https://www.zillow.com) property listing page. 

```python
username = 'username'
password = 'password'

payload = {
  'source': 'universal', #here we define source
  'url': 'https://www.zillow.com/homedetails/10066-Cielo-Dr-Beverly-Hills-CA-90210/243990393_zpid/'
}
```

4. Post Payload to the endpoint as per example below: [](https://realtime.oxylabs.io/v1/queries)

```python
import requests

username = 'username'
password = 'password'

payload = {
  'source': 'universal', 
  'url': 'https://www.zillow.com/homedetails/10066-Cielo-Dr-Beverly-Hills-CA-90210/243990393_zpid/'
}

response = requests.post('https://realtime.oxylabs.io/v1/queries', json = payload, auth = (username, password))
```

5. Real Estate Scraper API HTML response is inside `JSON`.Therefore, we need to access the `content` key.

```python
import requests

username = 'username'
password = 'password'

payload = {
  'source': 'universal',
  'url': 'https://www.zillow.com/homedetails/10066-Cielo-Dr-Beverly-Hills-CA-90210/243990393_zpid/'
}

response = requests.post('https://realtime.oxylabs.io/v1/queries', json = payload, auth = (username, password))

html_content = response.json()['results'][0]['content']
```

6. And we write HTML into file:

```python
import requests

username = 'username'
password = 'password'

payload = {
  'source': 'universal',
  'url': 'https://www.zillow.com/homedetails/10066-Cielo-Dr-Beverly-Hills-CA-90210/243990393_zpid/'
}

response = requests.post('https://realtime.oxylabs.io/v1/queries', json = payload, auth = (username, password))

html_content = response.json()['results'][0]['content']

with open ('scraped_website.html', 'w') as output:
  output.write(html_content)
```

After running the basic function, try adding parameters that will retrieve more specified data. 

7. Geo_location parameter will help you collect geo-restricted data for the websites that the content is only available to users from certain countries. 

```python
'geo_location': 'United States'
```

### Example:

```python
import requests

username = 'username'
password = 'password'

payload = {
  'source': 'universal', #here we define source
  'url': 'https://www.zillow.com/homedetails/10066-Cielo-Dr-Beverly-Hills-CA-90210/243990393_zpid/',
  'geo_location': 'United States'
}
 
response = requests.post('https://realtime.oxylabs.io/v1/queries', json = payload, auth = (username, password))

html_content = response.json()['results'][0]['content']

with open ('scraped_website.html', 'w') as output:
  output.write(html_content)
```

8. If the website uses JavaScript, use `render` parameter: 

```python
'render': 'html'
```

### Example:

```python
import requests
username = 'username'
password = 'password'

payload = {
  'source': 'universal', #here we define source
  'url': 'https://www.zillow.com/homedetails/10066-Cielo-Dr-Beverly-Hills-CA-90210/243990393_zpid/',
  'geo_location': 'United States',
  'render': 'html'
}

response = requests.post('https://realtime.oxylabs.io/v1/queries', json = payload, auth = (username, password))

html_content = response.json()['results'][0]['content']

with open ('scraped_website.html', 'w') as output:
  output.write(html_content)
```

9. Finally, you can use Real Estate Scraper API's [Scheduler](https://developers.oxylabs.io/scraper-apis/getting-started/scheduler-beta) feature to automate your recurring scraping jobs. The code example below will make the Scheduler run five jobs at 03:00 on Mondays until `end_time` (inclusive) and will return results to your chosen `callback_url`.


### Example:

```python
import requests
username = 'username'
password = 'password'
​
# Define a payload with some scraping jobs
payload = {
   'cron': '0 3 * * 1',
   'items': [
       {
           'source': 'universal',
           'url': 'https://www.zillow.com/homedetails/property1_zpid/',
           'geo_location': 'United States',
           'render': 'html',
           'callback_url': 'https://my.callback.url/endpoint1',
       },
       {
           'source': 'universal',
           'url': 'https://www.zillow.com/homedetails/property2_zpid/',
           'geo_location': 'United States',
           'render': 'html',
           'callback_url': 'https://my.callback.url/endpoint1',
       },
       {
           'source': 'universal',
           'url': 'https://www.zillow.com/homedetails/property3_zpid/',
           'geo_location': 'United States',
           'render': 'html',
           'callback_url': 'https://my.callback.url/endpoint1',
       },
       {
           'source': 'universal',
           'url': 'https://www.zillow.com/homedetails/property4_zpid/',
           'geo_location': 'United States',
           'render': 'html',
           'callback_url': 'https://my.callback.url/endpoint1',
       },
       {
           'source': 'universal',
           'url': 'https://www.zillow.com/homedetails/property5_zpid/',
           'geo_location': 'United States',
           'render': 'html',
           'callback_url': 'https://my.callback.url/endpoint1',
       },
   ],
   'end_time': '2032-12-21 12:34:45',
}
​
# Submit the payload
response = requests.request(
   'POST',
   'https://data.oxylabs.io/v1/schedules',
   auth=(username, password),
   json=payload,
)
​
# Print prettified response to stdout.
pprint(response.json())

```


## Conclusion

We hope this quick guide helped you understand how truly effortless it is to set up Oxylabs Real Estate Scraper API and how the integration process functions. 

Visit Oxylabs [documentation](https://developers.oxylabs.io/scraper-apis/real-estate-scraper-api) to find scraping guidelines for other real estate websites. In case you couldn't find the website you are interested in, get in touch with our support team via the 24/7 available live chat. We will discuss your use case and see if we can give you a personalized offer.
