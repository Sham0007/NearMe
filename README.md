# Ex04 Places Around Me
## Date: 26/04/2025

## AIM
To develop a website to display details about the places around my house.

## DESIGN STEPS

### STEP 1
Create a Django admin interface.

### STEP 2
Download your city map from Google.

### STEP 3
Using ```<map>``` tag name the map.

### STEP 4
Create clickable regions in the image using ```<area>``` tag.

### STEP 5
Write HTML programs for all the regions identified.

### STEP 6
Execute the programs and publish them.

## CODE
```
 views.py




 from django.shortcuts import render
 def map(request):
    return render(request,'Imagemapgpt.html')
 def abs(request):
    return render(request,'Absgpt.html')
 def hdfc(request):
    return render(request,'HDFCgpt.html')
 def poorvika(request):
    return render(request,'Poorvikagpt.html')
 def sarao(request):
    return render(request,'Saraogpt.html')

urls.py




 from django.contrib import admin
 from django.urls import path
 from map import views
 urlpatterns = [
    path('admin/', admin.site.urls),
    path('imagemap',views.map),
    path('Sarao_gpt.html',views.sarao),
    path('ABs_gpt.html',views.abs),
    path('Poorvika_gpt.html',views.poorvika),
    path('HDFC_gpt.html',views.hdfc),
 ]


settings.py





from pathlib import Path
 import os
 BASE_DIR = Path(__file__).resolve().parent.parent
 SECRET_KEY = 'django-insecure-1+xy#s7eou_u_2g5hvcu(ug1f-rd#=bfg^qo9=v)h!4dzt-vkk'
 DEBUG = True
 ALLOWED_HOSTS = []
 INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'map',
 ]
 MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
 ]
 ROOT_URLCONF = 'imagemap.urls'
 TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
 ]
 WSGI_APPLICATION = 'imagemap.wsgi.application'
 DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
 }
 AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
 ]
 LANGUAGE_CODE = 'en-us'
 TIME_ZONE = 'UTC'
 USE_I18N = True
 USE_TZ = True
 STATIC_URL = 'static/'
 DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'


imagemap.html





 <!DOCTYPE html>
 <html lang="en">
 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Porur Map</title>
    
    <!-- Font Import -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Alegreya:wght@400;700&display=swap" 
rel="stylesheet">
    
    <style>
        /* General Reset */
        body, html {
            margin: 0;
            padding: 0;
            font-family: "Alegreya", serif;
            background-color: #f4f4f9;
            color: #333;
        }
        /* Header Section */
        #header {
            text-align: center;
            padding: 40px 20px;
            background: linear-gradient(90deg, #004d99, #0073e6);
            color: #fff;
        }
        #header h1 {
            margin: 0;
            font-size: 3rem;
            text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);
        }
        /* Map Section */
        #map-container {
            position: relative;
            text-align: center;
            margin: 30px auto;
            padding: 20px;
            width: 90%;
            max-width: 1400px;
            background: #ffffff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            overflow: hidden; /* Prevents map from overflowing */
        }
        #map-container h2 {
            font-size: 2rem;
            color: #004d99;
            margin-bottom: 20px;
        }
        #map-container img {
            display: block; /* Removes inline whitespace */
            width: 100%; /* Ensures the map fits the container width */
            height: auto; /* Maintains aspect ratio */
            border-radius: 8px;
        }
        /* Interactivity for Map Areas */
        area {
            cursor: pointer;
            transition: transform 0.3s, filter 0.3s;
        }
        area:hover {
            transform: scale(1.1);
            filter: brightness(1.2);
        }
        /* Footer Section */
        #footer {
            margin-top: 30px;
            padding: 15px;
            text-align: center;
            background: linear-gradient(90deg, #004d99, #0073e6);
            color: #fff;
            font-size: 1rem;
            box-shadow: 0 -4px 8px rgba(0, 0, 0, 0.1);
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            #header h1 {
                font-size: 2.5rem;
            }
            #map-container h2 {
                font-size: 1.5rem;
            }
        }
    </style>
 </head>
 {% load static %}
 <body>
    <!-- Header -->
    <header id="header">
        <h1>Interactive Porur Map</h1>
    </header>
    <!-- Main Content -->
    <main>
        <section id="map-container">
            <h2>Explore Porur Landmarks</h2>
            <img src="{% static 'image/googlemap.png'%}" alt="Interactive Porur Map" 
usemap="#image-map">
            <map name="image-map">
                <area alt="Super Saravana Stores" title="Super Saravana Stores" 
href="Sarao_gpt.html" 
                      coords="650,8,603,172,605,203,643,205,672,200,719,14" shape="poly" aria
label="Super Saravana Stores">
                <area alt="Poorvika" title="Poorvika" href="Poorvika_gpt.html" 
                      
coords="664,299,665,315,670,331,675,340,671,356,670,370,682,372,687,365,702,334,705,317,705,298" 
shape="poly" aria-label="Poorvika">
                <area alt="HDFC Bank" title="HDFC Bank" href="HDFC_gpt.html" 
                      coords="907,208,899,226,902,242,919,251,936,258,951,248,965,225,939,204" 
shape="poly" aria-label="HDFC Bank">
                <area alt="AB's Restaurant" title="AB's Restaurant" href="ABs_gpt.html" 
                      
coords="620,665,617,690,633,697,665,700,685,702,700,680,700,660,680,642,649,631,631,640" 
shape="poly" aria-label="AB's Restaurant">
            </map>
        </section>
    </main>
    <!-- Footer -->
    <footer id="footer">
        &copy; 2024 Porur Map Interactive | Designed for Accessibility and Responsiveness
    </footer>
 </body>
 </html>



AB resraurant.html





<!DOCTYPE html>
 <html lang="en">
 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AB's Absolute Barbecues Restaurant</title>
    <style>
        /* General Reset */
        body, html {
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            background-color: #f9f9f9;
            color: #333;
        }
        /* Logo Section */
        #logo {
            text-align: center;
            padding: 20px;
            background-color: #333;
        }
        #logo img {
            max-width: 300px;
            height: auto;
        }
        /* About Section */
        #about {
            max-width: 1200px;
            margin: 50px auto;
            padding: 20px;
            background: #ffffff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        #about h1 {
            font-size: 2.5rem;
            color: #d35400;
            margin-bottom: 20px;
            border-bottom: 3px solid #f39c12;
            padding-bottom: 10px;
            text-align: center;
        }
        #about p {
            font-size: 1.2rem;
            line-height: 1.8;
            word-spacing: 3px;
            text-align: justify;
            margin: 20px;
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            #about p {
                font-size: 1rem;
                word-spacing: 2px;
            }
            #about h1 {
                font-size: 2rem;
            }
        }
        /* Additional Customizations */
        .highlight {
            color: #d35400;
            font-weight: bold;
        }
    </style>
 </head>
 {% load static %}
 <body>
    <!-- Logo Section -->
    <header id="logo">
        <img src="{% static 'image/abslogo.png'%}" alt="AB's Absolute Barbecues Logo">
    </header>
    <!-- About Section -->
    <section id="about">
        <h1>About Us</h1>
        <p>
            <span class="highlight">Absolute Barbecues</span> was born from pure passion. It 
begins with barbecues, and with it comes the idea of celebration. In fact, they are inseparable. 
So this is a place where people can have a blast without limits.
            <br><br>
            A buffet restaurant specialized in barbecue varieties, Indian cuisine, exotic meats, 
continental specials, and drool-worthy desserts. Here, you can come with your family and friends 
to have a gala time every day of the week if you so wish.
            <br><br>
            Popularising the concept of BBQ and reinventing it involved tremendous effort from 
our chefs and marketing minds. Today we are in a position to showcase a BBQ culture that’s 
widely loved and craved after. The buffet, combined with our wish grill, endless customisation 
options (Genie Chef), regular food festivals, exotic meat range and the widest selection of 
desserts make AB’s one of its kind. Wish grill is an irresistible attraction for any foodie out 
there. All AB’s outlets typically have a few dishes/meat/veg choices exclusively for wish-grill 
where customers could come and get their dish done the way they wish. A constant crowd puller 
and something that gourmands have come to love.
            <br><br>
            AB’s is designed for celebrations small and big. Our interiors take cue from 
carnival aesthetics with grand spaces, expansive seating and vibrant colours. The restaurant has 
conducted several food festivals, including Indian Street Food Festival, Brazilian Food Carnival 
and so on, introducing various dishes from rural India and all over the world.
            <br><br>
            AB's Express is the delivery wing of AB's, offering customised options such as 
Genie's Buffet Box, Meal-for-One, Starters Box, and festival special lunch/dinner offerings all 
carrying the signature AB's taste and flavour. The Genie's Buffet Box was a one-of-a-kind 
innovation that was designed to take the buffet experience home and has been a popular favourite 
ever since it was introduced. 
            <br><br>
            AB's barbecue buffet restaurant chain is headquartered in Hyderabad, India. Started 
in 2013 by restaurateur Prosenjit Roy Choudhury, the chain has 54 outlets in India and 3 in 
Dubai, 1 in Qatar.. We are rapidly expanding in response to growing demand for buffet dining 
along with our delivery service. 
            <br><br>
            <span class="highlight">That’s Absolute Barbecues.</span>
        </p>
    </section>
 </body>
 </html>



HDFCbank.html






 <!DOCTYPE html>
 <html lang="en">
 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HDFC Bank</title>
    <style>
        /* General Reset */
        body, html {
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            background-color: #eeeded;
            color: #333;
        }
        /* Logo Section */
        #logo {
            text-align: center;
            padding: 30px;
            background-color: #ffffff;
        }
        #logo img {
            max-width: 600px; /* Increased size for better visibility */
            height: auto;
        }
        /* About Section */
        #about {
            max-width: 1200px;
            margin: 50px auto;
            padding: 30px;
            background: #ffffff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            text-align: center;
        }
        #about h1 {
            font-size: 2.5rem;
            color: #003366;
            margin-bottom: 20px;
            border-bottom: 3px solid #ff3300; /* HDFC's red accent */
            padding-bottom: 10px;
        }
        #about p {
            font-size: 1.2rem;
            line-height: 1.8;
            word-spacing: 3px;
            text-align: justify;
            margin: 20px;
        }
        /* Highlight Important Text */
        .highlight {
            color: #ff3300;
            font-weight: bold;
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            #logo img {
                max-width: 300px; /* Scales down for smaller screens */
            }
            #about p {
                font-size: 1rem;
                word-spacing: 2px;
            }
            #about h1 {
                font-size: 2rem;
            }
        }
    </style>
 </head>
 {% load static %}
 <body>
    <!-- Logo Section -->
    <header id="logo">
        <img src="{% static 'image/hdfclogo.png'%}" alt="HDFC Bank Logo">
    </header>
    <!-- About Section -->
    <section id="about">
        <h1>About Us</h1>
        <p>
            The <span class="highlight">Housing Development Finance Corporation Limited</span>, 
or HDFC Ltd, was among the first financial institutions in India to receive an “in principle” 
approval from the Reserve Bank of India (RBI) to set up a bank in the private sector. This was 
part of RBI’s policy for liberalisation of the Indian banking industry in 1994.
            <br><br>
            On April 4, 2022 the merger of India’s largest Housing Finance Company, HDFC Limited 
and the largest private sector bank in India, HDFC Bank was announced. HDFC Ltd, over the last 
45 years has developed one of the best product offerings making it a leader in the housing 
finance business.
            <br><br>
            As of September 30, 2024, the Bank’s distribution network was at 9,092 branches and 
20,993 ATMs across 4,088 cities / towns as against 7,945 branches and 20,596 ATMs across 3,836 
cities / towns as of September 30, 2023. 51% of our branches are in semiurban and rural areas. 
The Bank’s international operations comprises four branches in Hong Kong, Bahrain, Dubai and an 
IFSC Banking Unit (IBU) in Gujarat International Finance Tech City. It has five representative 
offices in Kenya, Abu Dhabi, Dubai, London and Singapore
            <br><br>
            HDFC Bank’s mission is to be a world class Indian bank. We have a two-fold 
objective: first, to be the preferred provider of banking services for target retail and 
wholesale customer segments. The second objective is to achieve healthy growth in profitability, 
consistent with the bank’s risk appetite.
            <br><br>
            The bank is committed to maintaining the highest level of ethical standards, 
professional integrity, corporate governance and regulatory compliance. HDFC Bank’s business 
philosophy is based on five core values: Operational Excellence, Customer Focus, Product 
Leadership, People and Sustainability.
            <br><br>
            <span class="highlight">HDFC Bank</span> was incorporated in August 1994 in the name 
of HDFC Bank Limited, with its registered office in Mumbai, India. The bank commenced operations 
as a Scheduled Commercial Bank in January 1995.
        </p>
    </section>
 </body>
 </html>



poorvikamobiles.html






 <!DOCTYPE html>
 <html lang="en">
 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Poorvika Mobiles</title>
    <style>
        /* General Reset */
        body, html {
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            background-color: #e3e3e3;
            color: #333;
        }
        /* Logo Section */
        #logo {
            text-align: center;
            padding: 30px;
            background-color: #ffffff;
        }
        #logo img {
            max-width: 1000px;
            height: auto;
        }
        /* About Section */
        #about {
            max-width: 1200px;
            margin: 50px auto;
            padding: 30px;
            background: #ffffff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        #about h1 {
            font-size: 2.5rem;
            color: #ff6f00;
            text-align: center;
            margin-bottom: 20px;
            border-bottom: 3px solid #ffa500; /* Poorvika's theme orange */
            padding-bottom: 10px;
        }
        #about p {
            font-size: 1.2rem;
            line-height: 1.8;
            word-spacing: 2px;
            text-align: justify;
            margin: 20px;
        }
        /* Highlight Important Text */
        .highlight {
            color: #ff6f00;
            font-weight: bold;
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            #logo img {
                max-width: 600px; /* Scales down for smaller screens */
            }
            #about p {
                font-size: 1rem;
                word-spacing: 1px;
            }
            #about h1 {
                font-size: 2rem;
            }
        }
    </style>
 </head>
 {% load static %}
 <body>
    <!-- Logo Section -->
    <header id="logo">
        <img src="{% static 'image/poorvikalogo.png'%}" alt="Poorvika Mobiles Logo">
    </header>
    <!-- About Section -->
    <section id="about">
        <h1>About Us</h1>
        <p>
            <span class="highlight">Poorvika Mobiles Private Limited</span> is India’s leading 
mobile retailer with its wings wide spread in South India, and their reputation extends across 
the nation. Poorvika sells Mobile Phones & Tablets of domestic and international brands, Mobile 
Accessories, Data Cards, Earphones, Smart Watches, and much more. Driven by the mantra <span 
class="highlight">"Think Mobile, Think Poorvika"</span>, we have become a trusted name in the 
industry.
            <br><br>
            Poorvika Mobiles is located in Tamil Nadu, Pondicherry, Kerala, Karnataka, and 
Maharashtra. Headquartered in Chennai, India, the company provides a diverse range of services 
for gadget users. 
            <br><br>
            Poorvika Mobiles brings you Domestic & International brand mobile phones along with 
gadgets & accessories to complement its offerings at affordable prices, amazing quality, and 
dependable after-sale services. 
Saravanastores.html
            <br><br>
            Now boasting over 475 mobile stores and in Tamil Nadu Karnataka, Maharashtra, and 
Pondicherry & 12 home appliances stores across Chennai & Selam.
            The story of Poorvika Mobiles began in the early 2000s when the mobile industry was 
experiencing a dramatic transformation. The emergence of cell phones as a game-changing 
technology captured the attention of its founders. In an interview with the company's 
leadership, they revealed that their motivation to start Poorvika Mobiles was driven by the 
desire to explore this new and exciting product.
            <br><br>
            Poorvika doesn't hesitate to say that it is their beloved employees, or Poorvikans, 
as they address themselves, who are responsible for building and being the blood that drives 
this Empire that is spread across multiple states. The 4000+ Dedicated Staff who work together 
as a Family range from New Joiners who are yet to finish their first month here to Veteran Staff 
Members who have been part of the Poorvika Family for years and even decades.
            <br><br>
            Poorvika itself operates more like a Close-Knit Family rather than a Cold, 
Calculating Corporate, Putting the Needs, Well Being and Happiness of their Staff & Families 
over gains and profits. Everyone at Poorvika has a story of how the Company stood beside them in 
their time of need. Much like a Family, every Poorvikan works together, often at times 
Collaborating across Departments, Teams, and even States to bring the Idea of Poorvika into 
Reality. The Poorvika Family is famous for its readiness to help staff learn new skills, often 
sending Teams for Skill Building Classes and Conducting Exercises with Renowned Professionals.
            <br><br>
            Our reputation is built on a <span class="highlight">customer-friendly business 
pattern</span> and <span class="highlight">uncompromising quality</span> in both the Sales and 
Service sectors. We continue to strengthen our customer base across the country, fueled by our 
commitment to delivering excellence in all we do.
        </p>
    </section>
 </body>
 </html>



saravananstores.html






 <!DOCTYPE html>
 <html lang="en">
 <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Saravana Stores Porur</title>
    <style>
        /* General Reset */
        body, html {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            line-height: 1.6;
            background-color: #efecec;
            color: #333;
        }
        /* Logo Section */
        #logo {
            text-align: center;
            padding: 20px;
            background-color: #ffffff;
        }
        #logo img {
            max-width: 100%;
            height: auto;
        }
        /* About Section */
        #about {
            max-width: 1200px;
            margin: 50px auto;
            padding: 20px;
            background: #ffffff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        #about h1 {
            font-size: 2.5rem;
            color: #004d99;
            margin-bottom: 20px;
            border-bottom: 3px solid #ff9900;
            padding-bottom: 10px;
            text-align: center;
        }
        #about p {
            font-size: 1.2rem;
            line-height: 1.8;
            word-spacing: 3px;
            text-align: justify;
            margin: 0 20px;
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            #about p {
                font-size: 1rem;
                word-spacing: 2px;
            }
            #about h1 {
                font-size: 2rem;
            }
        }
    </style>
 </head>
 {% load static %}
 <body>
    <!-- Logo Section -->
    <header id="logo">
        <img src="{% static 'image/saraologo.png'%}" alt="Saravana Stores Logo">
    </header>
    <!-- About Section -->
    <section id="about">
        <h1>About Us</h1>
        <p>
            Saravana Stores, founded in 1969, is a chain of retail stores in India. It is the 
largest family-owned business retail chain in India and the first to introduce the Aadi 
Thallupadi sale concept.
            <br><br>
            A success story built on hard work, sound business practices, and dynamism, guided 
by visionary management. Through the continuous patronage of customers, Saravana Stores has 
become a fantasy land of shopping, located at T. Nagar, Purasawalkam, Chrompet, and Porur. A 
fairy tale woven in fabrics of love, quality, elegance, and allure has captured the hearts of 
loyal clientele over the decades. Walk in for a truly pleasurable shopping experience.
            <br><br>
            Saravana Stores offers a paradise of textiles with an unbeatable range of clothing, 
garments, and accessories that cater to every family member at unbelievable prices. Choose from 
a vast selection of:
        </p>
        <ul style="font-size: 1.2rem; line-height: 1.8; padding-left: 40px;">
            <li>Gold, Diamond Jewelry, and Silver articles</li>
            <li>Chudidhars, Silk Sarees, Wedding Collections, Gaghras, Lehengas, Designer 
Sarees, and Blouses</li>
            <li>Men’s Wear, Suiting Shirting, Kids’ Wear, and Accessories</li>
            <li>Furniture, Electronics, Toys, Sports Equipment, and Home Appliances</li>
            <li>Footwear, Groceries, Cosmetics, Perfumes, and much more</li>
        </ul>
        <p>
            Whatever is on your shopping list, Saravana Stores has an answer. With a large 
selection of leading brands, fashionable patterns, and designer items, Saravana Stores is the 
ultimate shopping destination.
        </p>
    </section>
 </body>
 </html>
```


  

    


## OUTPUT

![image](https://github.com/user-attachments/assets/0cf06d4b-db53-4a37-aebc-af67ce1b8b8c)

![image](https://github.com/user-attachments/assets/494da210-b08b-463a-9d67-92eb166d298c)

![image](https://github.com/user-attachments/assets/3f0772e6-0773-4fa7-83c9-3a58fdc8be7f)

![image](https://github.com/user-attachments/assets/3a37fc6a-caee-4164-be41-8d76631a9a23)





## RESULT
The program for implementing image maps using HTML is executed successfully.
