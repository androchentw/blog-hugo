# GenAI Cloud Run | K8s Summit 2024 GCP Workshop

## Preparation

* [Deploy a Streamlit App Integrated with Gemini Pro on Cloud Run | GSP1229](https://explore.qwiklabs.com/classrooms/16139/labs/95581)
  * [generative-ai/gemini/sample-apps/gemini-streamlit-cloudrun/app.py](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/sample-apps/gemini-streamlit-cloudrun/app.py)

[Gemini](https://deepmind.google/technologies/gemini/#introduction) is a family of generative AI models developed by Google DeepMind that is designed for multimodal use cases. The Gemini API gives you access to the Gemini Pro Vision and Gemini Pro models. In this lab you will understand how to integrate Vertex AI Gemini API with applications and build and deploy the developed sample application on Google Cloud Run.

### Vertex AI Gemini API

The Vertex AI Gemini API provides a unified interface for interacting with Gemini models. There are currently two models available in the Gemini API:

1. Gemini Pro model (gemini-pro): Designed to handle natural language tasks, multiturn text and code chat, and code generation.
2. Gemini Pro Vision model (gemini-pro-vision): Supports multimodal prompts. You can include text, images, and video in your prompt requests and get text or code responses.

You can interact with the Gemini API using the following methods:

* Use the Vertex AI Studio for quick testing and command generation
* Use cURL commands
* Use the Vertex AI SDK

This lab focuses on integrating the Gemini Pro model with a Streamlit application and deploying the application on Google Cloud Run.

For more information, see the [Generative AI on Vertex AI](https://cloud.google.com/vertex-ai/docs/generative-ai/learn/overview) documentation.

### Objectives

* Integrate Vertex AI Gemini API with applications
* Build and deploy the developed sample application on Google Cloud Run
* Use the Streamlit framework to build a Cloud Run application

## Task 1. Run the Application Locally

```sh
git clone https://github.com/GoogleCloudPlatform/generative-ai.git

cd generative-ai/gemini/sample-apps/gemini-streamlit-cloudrun

python3 -m venv gemini-streamlit
source gemini-streamlit/bin/activate
pip install -r requirements.txt

GCP_PROJECT='qwiklabs-gcp-03-07752b0f928b'
GCP_REGION='us-central1'

streamlit run app.py \
  --browser.serverAddress=localhost \
  --server.enableCORS=false \
  --server.enableXsrfProtection=false \
  --server.port 8080
```

<img style="width:80%;" src="https://cdn.qwiklabs.com/yOGqSZeJiSUjvhAYVEcg2EbGGakL6QY6CVLLt%2FeA4Vk%3D">

### Generate story

```prompt
Parameters:
- Temperature: 0.3
- Max Output Tokens: 2048
Write a Short story based on the following premise: 

    character_name: Mittens 

    character_type: Cat 

    character_persona: Mittens is a very friendly cat. 

    character_location: Andromeda Galaxy 

    story_premise: Love,Adventure 

    If the story is "short", then make sure to have 5 chapters or else if it is "long" then 10 chapters.
    Important point is that each chapters should be generated based on the premise given above.
    First start by giving the book introduction, chapter introductions and then each chapter. It should also have a proper ending.
    The book should have prologue and epilogue.
```

```txt
Your story:

Mittens in Andromeda: A Purrfectly Galactic Adventure
Prologue:

Mitt ens, a fluffy ginger tabby with eyes like melted gold, was no ordinary cat. While her brethren were content with chasing mice and napping in sunbeams, Mittens dreamt of stars. She spent countless hours gazing at the night sky from her perch on the windowsill, her whiskers twitching with a yearning for the unknown. Little did she know, her destiny lay beyond the familiar confines of her Earthly home.

Chapter 1: The Cosmic Catnap

Mittens was dozing peacefully in her favorite sunbeam when a strange hum vibrated through the air. She opened one eye, then the other, and saw a shimmering portal opening in the living room. Curiosity overcame her usual feline caution. She cautiously approached the portal, her tail twitching with anticipation. A gentle breeze, infused with the scent of stardust, wafted from within. With a playful flick of her tail, Mittens stepped through the portal, leaving her familiar world behind.

Chapter 2: A Purrfectly Strange New World

The portal deposited Mittens in a vibrant, alien landscape. Lush, bioluminescent plants swayed in the gentle breeze, and strange, winged creatures flitted through the air. The air hummed with a symphony of unfamiliar sounds. Mittens, ever the explorer, cautiously ventured into this strange new world, her whiskers twitching with excitement. She encountered a group of furry, bipedal creatures with large, curious eyes. They greeted her with soft chirps and gentle touches, their language a melody of clicks and whistles.

Chapter 3: The Galactic Meow-ster

Mittens quickly learned that these creatures, the "Zylorians," were peaceful and kind. They welcomed her into their community, fascinated by her unique appearance and playful nature. They named her "Mittens," a sound that resonated with their own language . Mittens, in turn, found herself drawn to their gentle ways and their love for all creatures, big and small. She learned their language, their customs, and their history, all the while sharing her own stories of Earth.

Chapter 4: The Whispers of the Stars

One night, while gazing at the Andromeda Galaxy, Mittens felt a strange pull. She heard whispers in the wind, faint but insistent, urging her to follow the stars. The Zylorians, sensing her unease, explained that she was destined for a greater purpose, a mission that would unite the galaxies. They gifted her a special necklace, a shimmering orb that pulsed with cosmic energy. It was a beacon, a guide to her true destiny.

Chapter 5: The Cosmic Cat-astrophe

Following the whispers of the stars, Mittens embarked on a journey across the Andromeda Galaxy. She encountered strange and wonderful creatures, each with their own unique stories and struggles. She used her friendly nature and her newfound cosmic powers to help those in need, spreading peace and understanding wherever she went. But her journey was not without its challenges. A dark force, fueled by fear and greed, threatened to plunge the galaxy into chaos.

Epilogue:

Mittens, with the help of her Zylorian friends and the power of the stars, confronted the dark force and triumphed. She brought peace and harmony to the Andromeda Galaxy, proving that even a small cat from Earth could make a difference. She returned to her home planet, forever changed by her adventures. She continued to share her stories, inspiring others to embrace the unknown and to believe in the power of love and friendship, even across the vast expanse of the cosmos.
```

### Marketing Campaign

```prompt
Generate a marketing campaign for ZomZoo, a Clothing designed for the age group: 18-24.
    The target location is this: Urban.
    Aim to primarily achieve ['Increase brand awareness', 'Generate leads'].
    Emphasize the product's unique selling proposition while using a Formal tone of voice.
    Allocate the total budget of 1,000-5,000.
    With these inputs, make sure to follow following guidelines and generate the marketing campaign with proper headlines: 

    - Briefly describe company, its values, mission, and target audience.
    - Highlight any relevant brand guidelines or messaging frameworks.
    - Provide a concise overview of the campaign's objectives and goals.
    - Briefly explain the product or service being promoted.
    - Define your ideal customer with clear demographics, psychographics, and behavioral insights.
    - Understand their needs, wants, motivations, and pain points.
    - Clearly articulate the desired outcomes for the campaign.
    - Use SMART goals (Specific, Measurable, Achievable, Relevant, and Time-bound) for clarity.
    - Define key performance indicators (KPIs) to track progress and success.
    - Specify the primary and secondary goals of the campaign.
    - Examples include brand awareness, lead generation, sales growth, or website traffic.
    - Clearly define what differentiates your product or service from competitors.
    - Emphasize the value proposition and unique benefits offered to the target audience.
    - Define the desired tone and personality of the campaign messaging.
    - Identify the specific channels you will use to reach your target audience.
    - Clearly state the desired action you want the audience to take.
    - Make it specific, compelling, and easy to understand.
    - Identify and analyze your key competitors in the market.
    - Understand their strengths and weaknesses, target audience, and marketing strategies.
    - Develop a differentiation strategy to stand out from the competition.
    - Define how you will track the success of the campaign.
   -  Utilize relevant KPIs to measure performance and return on investment (ROI).
   Give proper bullet points and headlines for the marketing campaign. Do not produce any empty lines.
   Be very succinct and to the point.
```

```text
ZomZoo: Urban Style, Elevated[](https://8080-cs-c218f025-ba48-45ef-962f-f47f330fae4d.ql-asia-east1-riws.cloudshell.dev/?authuser=0&redirectedPreviously=true#zomzoo-urban-style-elevated)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Company Description: ZomZoo is a clothing brand that caters to the bold and stylish urban youth aged 18-24. We prioritize quality materials, unique designs, and ethical manufacturing practices.

Values: ZomZoo embodies individuality, self-expression, and social responsibility.

Mission: To empower the next generation with clothing that reflects their unique style and values.

Target Audience:

-   Demographics: 1 8-24 years old, urban dwellers, both male and female.
-   Psychographics: Trend-conscious, socially aware, value quality and ethical sourcing, enjoy expressing their individuality, active social media users.
-   Behavioral Insights: Frequent online shoppers, influenced by social media trends, enjoy discovering new brands, engaged with sustainability initiatives.

Campaign Objectives:

-   Primary: Increase brand awareness among the target audience.
-   Secondary : Generate leads and drive traffic to our website.

Product: ZomZoo offers a curated collection of streetwear-inspired clothing, featuring bold graphics, sustainable materials, and innovative designs.

Unique Selling Proposition:

-   Elevated Streetwear: ZomZoo combines street style with a refined edge, offering a unique blend of comfort, style, and quality.
-   Ethical Sourcing: We prioritize sustainable materials and ethical manufacturing practices, ensuring responsible production.
-   Individuality & Expression: Our designs empower wearers to showcase their unique style and express their individuality.

Campaign Tone: Modern, confident, edgy, and aspirational.

Campaign Messaging:

-   Headline: "ZomZoo: Where Style Meets Sustainability."
-   Tagline: "Express Yourself. Own Your Style."
-   Key Messages:
    -   High-quality, comfortable, and stylish clothing designed for the urban youth.
    -   Unique designs that empower individuality and self-expression.
    -   Committed to ethical sourcing and sustainable practices.

Campaign Channels:

-   Social Media: Instagram, TikTok, Facebook (targeted ads)
-   Influencer Marketing: Collaborate with micro-influencers in the fashion and sustainability space.
-   Content Marketing: Create engaging blog posts, articles, and videos focusing on style, sustainability, and social responsibility.
-   Email Marketing: Build an email list and send targeted email campaigns with exclusive offers and content.

Call to Action:

-   Website: Visit our website to browse our latest collection and shop now.
-   Social Media: Follow us on social media for style inspiration and exclusive offers.
-   Sign Up: Join our email list to receive updates on new arrivals and exclusive promotions.

Competitor Analysis:

-   Key Competitors: Urban Outfitters, ASOS, H&M, Everlane, Reformation.
-   Differentiation Strategy: Focus on ethical sourcing, unique designs, and a community-driven approach to style and sustainability.

Campaign Tracking:

-   KPIs: Website traffic, social media engagement (likes, shares, comments), lead generation through website forms and social media contests, brand mentions, website conversion rate, email list growth.

Campaign Budget: $2,500 (allocated as follows):

-   Social Media Ads: $1,000
-   Influencer Marketing: $500
-   ** Content Creation:** $500
-   Email Marketing Tool: $500

SMART Goals:

-   Increase brand awareness by 20% within 3 months.
-   Generate 500 leads through website and social media forms within 3 months.
-   Increase website traffic by 15% within 3 months.

Success Measurement: Track KPIs through analytics dashboards and reports. Analyze the campaign's performance, adjust strategies based on insights, and optimize for maximum ROI.
```

### Image Playground

<img style="width:80%;" src="https://storage.googleapis.com/github-repo/img/gemini/multimodality_usecases_overview/er.png">

```text
The ER diagram depicts a database for a beverage store chain. The entities are:

-   Category : Represents different categories of beverages, such as beer, wine, or spirits.
-   Vendor: Represents the suppliers of the beverages.
-   Item: Represents the individual beverage products sold by the store.
-   Sales: Represents the sales transactions made by the store.
-   County: Represents the geographical location of the store.
-   Convenience_store: Represents a type of store that sells convenience goods, including beverages.
-   Store: Represents the physical store locations of the chain.

The relationships between the entities are:

-   Category to Sales: A many-to-many relationship, indicating that a category can have many sales transactions, and a sales transaction can involve multiple categories.
-   Vendor to Sales: A many-to-many relationship, indicating that a vendor can supply multiple sales transactions, and a sales transaction can involve multiple vendors.
-   Item to Sales: A many-to-many relationship, indicating that an item can be sold in multiple sales transactions, and a sales transaction can involve multiple items.
-   County to Store: A one-to-many relationship, indicating that a county can have multiple stores, but a store can only be located in one county.
-   Convenience_store to Store: A one-to-one relationship, indicating that a convenience store is a specific type of store.
-   Sales to Convenience_store: A one-to-one relationship, indicating that a sales transaction can only be associated with one convenience store.

The primary keys (PK) for each entity are:

-   Category: category
-   Vendor: vendor_no
-   Item: item
-   Sales: None (composite key of date, store, category, vendor_no, item)
-   County: county_number
-   Convenience_store: store
-   Store: store

This ER diagram provides a comprehensive representation of the relationships between different entities in the beverage store chain database. It allows for efficient data management and analysis of sales, inventory, and store locations.
```

### Video Playground - 1

https://storage.googleapis.com/github-repo/img/gemini/multimodality_usecases_overview/mediterraneansea.mp4

```prompt
Prompt used:

Describe what is happening in the video and answer the following questions:

- What am I looking at? 

        - Where should I go to see it? 

        - What are other top 5 places in the world that look like this?

{video_data}
```

```text
The video shows an aerial view of a harbor in a coastal town. The camera is facing the harbor, which is protected by a breakwater. There are several boats docked in the harbor, and a few people are walking along the breakwater. The town is built on the cliffs overlooking the harbor. The sea is a beautiful turquoise color, and the waves are crashing against the breakwater.

-   What am I looking at? You are looking at the harbor of Antalya, Turkey.

-   Where should I go to see it? You should go to Antalya, Turkey.

-   What are other top 5 places in the world that look like this?

Here are 5 places in the world that look similar to the harbor of Antalya:

1.  Dubrovnik, Croatia: Dubrovnik is a walled city on the Adriatic Sea, known for its stunning harbor and medieval architecture.
2.  Santorini, Greece: Santorini is a volcanic island in the Aegean Sea, famous for its white-washed villages perched on cliffs overlooking the caldera.
3.  Positano, Italy: Positano is a colorful town on the Amalfi Coast, known for its steep cliffs and picturesque harbor.
4.  Vernazza, Italy: Vernazza is one of the five villages that make up Cinque Terre, a UNESCO World Heritage Site in Italy. It is known for its colorful houses and charming harbor.
5.  Rio de Janeiro, Brazil: Rio de Janeiro is a vibrant city on the Atlantic coast of Brazil, known for its iconic Sugarloaf Mountain and Copacabana Beach.
```

### Video Playground - 2

https://storage.googleapis.com/github-repo/img/gemini/multimodality_usecases_overview/pixel8.mp4

```prompt
Answer the following questions using the video only: What is the profession of the girl in this video? Which all features of the phone are highlighted here? Summarize the video in one paragraph. Provide the answer in table format.

{video_data}
```

| Question | Answer |
| --- | --- |
| What is the profession of the girl in this video? | Photographer |
| Which all features of the phone are highlighted here? | Video Boost and Night Sight |
| Summarize the video in one paragraph. | The video showcases the features of the new Pixel phone. The girl , a photographer in Tokyo, highlights the Video Boost feature which activates Night Sight in low light to enhance the quality of the video. She then takes videos of different places in Tokyo, including Sancha, where she first moved to Tokyo, and Shibuya, a popular district in Tokyo. |

## Task 2. Build and Deploy the Application to Cloud Run

```sh
# create another Cloud Shell tab
cd generative-ai/gemini/sample-apps/gemini-streamlit-cloudrun
GCP_PROJECT='qwiklabs-gcp-03-07752b0f928b'
GCP_REGION='us-central1'

AR_REPO='gemini-repo'
SERVICE_NAME='gemini-streamlit-app' 
gcloud artifacts repositories create "$AR_REPO" --location="$GCP_REGION" --repository-format=Docker
gcloud builds submit --tag "$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME"

gcloud run deploy "$SERVICE_NAME" \
  --port=8080 \
  --image="$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME" \
  --allow-unauthenticated \
  --region=$GCP_REGION \
  --platform=managed  \
  --project=$GCP_PROJECT \
  --set-env-vars=GCP_PROJECT=$GCP_PROJECT,GCP_REGION=$GCP_REGION

# Deploying container to Cloud Run service [gemini-streamlit-app] in project [qwiklabs-gcp-03-07752b0f928b] region [us-central1]     
# Service [gemini-streamlit-app] revision [gemini-streamlit-app-00001-mlj] has been deployed and is serving 100 percent of traffic.
# Service URL: https://gemini-streamlit-app-949781657808.us-central1.run.app
```

## Ref

* Check out the [Generative AI on Vertex AI documentation](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/overview).
* Learn more about Generative AI on the [Google Cloud Tech YouTube channel](https://www.youtube.com/@googlecloudtech).
* [Google Cloud Generative AI official repo](https://github.com/GoogleCloudPlatform/generative-ai)
* [Example Gemini notebooks](https://github.com/GoogleCloudPlatform/generative-ai/tree/main/gemini)
