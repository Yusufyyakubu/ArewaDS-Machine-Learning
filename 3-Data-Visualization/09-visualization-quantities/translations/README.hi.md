# विज़ुअलाइज़िंग मात्रा

|![ सकेटच्नोते करने वाला [(@sketchthedocs)](https://sketchthedocs.dev) ](../../sketchnotes/09-Visualizing-Quantities.png)|
|:---:|
| विज़ुअलाइज़िंग मात्रा - _सकेटच्नोते करने वाला [@nitya](https://twitter.com/nitya)_ |

इस पाठ में आप यह पता लगाएंगे कि मात्रा की अवधारणा के चारों ओर दिलचस्प विज़ुअलाइज़ेशन कैसे बनाएं, यह जानने के लिए कई उपलब्ध पायथन पुस्तकालयों में से एक का उपयोग कैसे करें। मिनेसोटा के पक्षियों के बारे में साफ किए गए डेटासेट का उपयोग करके, आप स्थानीय वन्यजीवों के बारे में कई रोचक तथ्य जान सकते हैं। 
## [प्री-रीडिंग क्विज](https://purple-hill-04aebfb03.1.azurestaticapps.net/quiz/16)

## माटप्लोटलिब के साथ पंखों का निरीक्षण करें

सरल और परिष्कृत दोनों प्रकार के प्लॉट और विभिन्न प्रकार के चार्ट बनाने के लिए एक उत्कृष्ट पुस्तकालय है [माटप्लोटलिब](https://matplotlib.org/stable/index.html)। सामान्य शब्दों में, इन पुस्तकालयों का उपयोग करके डेटा को प्लॉट करने की प्रक्रिया में आपके डेटाफ़्रेम के उन हिस्सों की पहचान करना शामिल है जिन्हें आप लक्षित करना चाहते हैं, उस डेटा पर कोई भी आवश्यक परिवर्तन करना, इसके x और y अक्ष मान निर्दिष्ट करना, यह तय करना कि किस प्रकार का प्लॉट दिखाना है, और फिर साजिश दिखा रहा है। माटप्लोटलिब विज़ुअलाइज़ेशन की एक विशाल विविधता प्रदान करता है, लेकिन इस पाठ के लिए, आइए उन पर ध्यान केंद्रित करें जो मात्रा को देखने के लिए सबसे उपयुक्त हैं: लाइन चार्ट, स्कैटरप्लॉट और बार प्लॉट।

> ✅ अपने डेटा की संरचना और जो कहानी आप बताना चाहते हैं, उसके अनुरूप सर्वोत्तम चार्ट का उपयोग करें। 
> - समय के साथ रुझानों का विश्लेषण करने के लिए: लाइन
> - मानों की तुलना करने के लिए: बार, कॉलम, पाई, स्कैटरप्लॉट
> - यह दिखाने के लिए कि भाग किस प्रकार संपूर्ण से संबंधित हैं: पाई
> - डेटा का वितरण दिखाने के लिए: स्कैटरप्लॉट, बार
> - रुझान दिखाने के लिए: लाइन, कॉलम
> - मानों के बीच संबंध दिखाने के लिए: लाइन, स्कैटरप्लॉट, बबल

यदि आपके पास एक डेटासेट है और यह पता लगाने की आवश्यकता है कि किसी दिए गए आइटम में से कितना शामिल है, तो आपके पास सबसे पहले कार्यों में से एक इसके मूल्यों का निरीक्षण करना होगा। 

✅ माटप्लोटलिब के लिए बहुत अच्छी 'चीट शीट' उपलब्ध हैं [here](https://matplotlib.org/cheatsheets/cheatsheets.pdf).

## बर्ड विंगस्पैन मूल्यों के बारे में एक लाइन प्लॉट बनाएं

इस पाठ फ़ोल्डर के मूल में `नोटबुक.आईपीएनबी` फ़ाइल खोलें और एक सेल जोड़ें।

> नोट: डेटा इस रेपो की जड़ में `/आंकड़े` फ़ोल्डर में संग्रहीत है।

```python
import pandas as pd
import matplotlib.pyplot as plt
birds = pd.read_csv('../../data/birds.csv')
birds.head()
```
यह डेटा टेक्स्ट और संख्याओं का मिश्रण है:


|      | नाम                         | वैज्ञानिक नाम        | श्रेणी              | आदेश        | परिवार   | जाति       | संरक्षण की स्थिति | न्यूनतम लंबाई | अधिकतम लंबाई | मिनबॉडीमास | मैक्सबॉडीमास | मिनविंगस्पैन | मैक्सविंगस्पैन |
| ---: | :--------------------------- | :--------------------- | :-------------------- | :----------- | :------- | :---------- | :----------------- | --------: | --------: | ----------: | ----------: | ----------: | ----------: |
|    0 | ब्लैक-बेल्ड सीटी-बतख | डेंड्रोसाइग्ना ऑटमलिस | बतख / गीज़ / जलपक्षी | अंसेरी फॉर्म्स | अनाटिडे | डेंड्रोसाइग्ना | एल सी                 |        47 |        56 |         652 |        1020 |          76 |          94 |
|    1 | फुल्वस सीटी-बतख       | डेंड्रोसाइग्ना बाइकलर    | बतख / गीज़ / जलपक्षी | अंसेरी फॉर्म्स | अनाटिडे | डेंड्रोसाइग्ना | एल सी                 |        45 |        53 |         712 |        1050 |          85 |          93 |
|    2 | हिम हंस                   | Anser caerulescens     | बतख / गीज़ / जलपक्षी | अंसेरी फॉर्म्स | अनाटिडे | Anser       | एल सी                 |        64 |        79 |        2050 |        4050 |         135 |         165 |
|    3 | रॉस हंस                 | Anser rossii           | बतख / गीज़ / जलपक्षी | अंसेरी फॉर्म्स | अनाटिडे | Anser       | एल सी                 |      57.3 |        64 |        1066 |        1567 |         113 |         116 |
|    4 | ग्रेटर व्हाइट-फ्रंटेड गूज  | Anser albifrons        | बतख / गीज़ / जलपक्षी | अंसेरी फॉर्म्स | अनाटिडे | Anser       | एल सी                 |        64 |        81 |        1930 |        3310 |         130 |         165 |

आइए बुनियादी लाइन प्लॉट का उपयोग करके कुछ संख्यात्मक डेटा को प्लॉट करके शुरू करें। मान लीजिए आप इन दिलचस्प पक्षियों के लिए अधिकतम पंखों का दृश्य चाहते हैं।

```python
wingspan = birds['MaxWingspan'] 
wingspan.plot()
```
![मैक्स विंगस्पैन](images/max-wingspan.png)

आप तुरंत क्या नोटिस करते हैं? ऐसा लगता है कि कम से कम एक बाहरी है - वह काफी पंख है! एक २३०० सेंटीमीटर पंखों का फैलाव २३ मीटर के बराबर होता है - क्या मिनेसोटा में पटरोडैक्टाइल घूम रहे हैं? आइए जांच करते हैं।

जबकि आप उन आउटलेर्स को खोजने के लिए एक्सेल में एक त्वरित सॉर्ट कर सकते हैं, जो शायद टाइपो हैं, प्लॉट के भीतर से काम करके विज़ुअलाइज़ेशन प्रक्रिया जारी रखें।

प्रश्न में किस प्रकार के पक्षी हैं, यह दिखाने के लिए x-अक्ष में लेबल जोड़ें:

```
plt.title('Max Wingspan in Centimeters')
plt.ylabel('Wingspan (CM)')
plt.xlabel('Birds')
plt.xticks(rotation=45)
x = birds['Name'] 
y = birds['MaxWingspan']

plt.plot(x, y)

plt.show()
```
![लेबल के साथ विंगस्पैन](images/max-wingspan-labels.png)

यहां तक ​​कि लेबल के रोटेशन को 45 डिग्री पर सेट करने के बाद भी, पढ़ने के लिए बहुत कुछ है। आइए एक अलग रणनीति का प्रयास करें: केवल उन आउटलेर्स को लेबल करें और चार्ट के भीतर लेबल सेट करें। लेबलिंग के लिए अधिक जगह बनाने के लिए आप स्कैटर चार्ट का उपयोग कर सकते हैं:

```python
plt.title('Max Wingspan in Centimeters')
plt.ylabel('Wingspan (CM)')
plt.tick_params(axis='both',which='both',labelbottom=False,bottom=False)

for i in range(len(birds)):
    x = birds['Name'][i]
    y = birds['MaxWingspan'][i]
    plt.plot(x, y, 'bo')
    if birds['MaxWingspan'][i] > 500:
        plt.text(x, y * (1 - 0.05), birds['Name'][i], fontsize=12)
    
plt.show()
```
यहाँ क्या चल रहा है? आपने निचले लेबल को छिपाने के लिए `tick_params` का उपयोग किया और फिर अपने पक्षियों के डेटासेट पर एक लूप बनाया। 'बो' का उपयोग करके छोटे गोल नीले डॉट्स वाले चार्ट को प्लॉट करते हुए, आपने 500 से अधिक पंखों वाले किसी भी पक्षी की जाँच की और यदि ऐसा है तो डॉट के बगल में उनका लेबल प्रदर्शित किया। आप y अक्ष (`वाई * (1 - 0.05)`) पर लेबल को थोड़ा सा ऑफसेट करते हैं और एक लेबल के रूप में पक्षी के नाम का उपयोग करते हैं।

आपने क्या खोजा?

![बाहरी कारकों के कारण](images/labeled-wingspan.png)
## अपना डेटा फ़िल्टर करें

बाल्ड ईगल और प्रेयरी फाल्कन दोनों, जबकि शायद बहुत बड़े पक्षी, गलत लेबल वाले प्रतीत होते हैं, उनके अधिकतम पंखों में अतिरिक्त `0` जोड़ा जाता है। यह संभावना नहीं है कि आप 25 मीटर पंखों वाले बाल्ड ईगल से मिलेंगे, लेकिन यदि ऐसा है, तो कृपया हमें बताएं! आइए उन दो आउटलेर्स के बिना एक नया डेटाफ़्रेम बनाएं:

```python
plt.title('Max Wingspan in Centimeters')
plt.ylabel('Wingspan (CM)')
plt.xlabel('Birds')
plt.tick_params(axis='both',which='both',labelbottom=False,bottom=False)
for i in range(len(birds)):
    x = birds['Name'][i]
    y = birds['MaxWingspan'][i]
    if birds['Name'][i] not in ['Bald eagle', 'Prairie falcon']:
        plt.plot(x, y, 'bo')
plt.show()
```

आउटलेर्स को फ़िल्टर करके, आपका डेटा अब अधिक सुसंगत और समझने योग्य है।

![पंखों का बिखराव](images/scatterplot-wingspan.png)

अब जबकि हमारे पास कम से कम पंखों के मामले में एक क्लीनर डेटासेट है, तो आइए इन पक्षियों के बारे में और जानें।

जबकि लाइन और स्कैटर प्लॉट डेटा मानों और उनके वितरण के बारे में जानकारी प्रदर्शित कर सकते हैं, हम इस डेटासेट में निहित मूल्यों के बारे में सोचना चाहते हैं। आप मात्रा के बारे में निम्नलिखित प्रश्नों के उत्तर देने के लिए विज़ुअलाइज़ेशन बना सकते हैं:

> पक्षियों की कितनी श्रेणियां हैं और उनकी संख्या क्या है?
> कितने पक्षी विलुप्त, संकटग्रस्त, दुर्लभ या सामान्य हैं?
> लिनिअस की शब्दावली में विभिन्न जीनस और आदेश कितने हैं?
## बार चार्ट का अन्वेषण करें

बार चार्ट व्यावहारिक होते हैं जब आपको डेटा के समूह दिखाने की आवश्यकता होती है। आइए इस डेटासेट में मौजूद पक्षियों की श्रेणियों का पता लगाएं, यह देखने के लिए कि संख्या के हिसाब से कौन सा सबसे आम है।

नोटबुक फ़ाइल में, एक मूल बार चार्ट बनाएं

✅ ध्यान दें, आप या तो पिछले अनुभाग में पहचाने गए दो बाहरी पक्षियों को फ़िल्टर कर सकते हैं, उनके पंखों में टाइपो को संपादित कर सकते हैं, या उन्हें इन अभ्यासों के लिए छोड़ सकते हैं जो पंखों के मूल्यों पर निर्भर नहीं करते हैं।

यदि आप एक बार चार्ट बनाना चाहते हैं, तो आप उस डेटा का चयन कर सकते हैं जिस पर आप ध्यान केंद्रित करना चाहते हैं। कच्चे डेटा से बार चार्ट बनाए जा सकते हैं:

```python
birds.plot(x='Category',
        kind='bar',
        stacked=True,
        title='Birds of Minnesota')

```
![बार चार्ट के रूप में पूर्ण डेटा](images/full-data-bar.png)

हालांकि, यह बार चार्ट अपठनीय है क्योंकि इसमें बहुत अधिक गैर-समूहीकृत डेटा है। आपको केवल उस डेटा का चयन करने की आवश्यकता है जिसे आप प्लॉट करना चाहते हैं, तो आइए उनकी श्रेणी के आधार पर पक्षियों की लंबाई देखें।

केवल पक्षी की श्रेणी को शामिल करने के लिए अपना डेटा फ़िल्टर करें।

✅ ध्यान दें कि आप डेटा को प्रबंधित करने के लिए पंडों का उपयोग करते हैं, और फिर माटप्लोटलिब को चार्टिंग करने दें।

चूंकि कई श्रेणियां हैं, आप इस चार्ट को लंबवत रूप से प्रदर्शित कर सकते हैं और सभी डेटा के हिसाब से इसकी ऊंचाई को बदल सकते हैं:

```python
category_count = birds.value_counts(birds['Category'].values, sort=True)
plt.rcParams['figure.figsize'] = [6, 12]
category_count.plot.barh()
```
![श्रेणी और लंबाई](images/category-counts.png)

यह बार चार्ट प्रत्येक श्रेणी में पक्षियों की संख्या का एक अच्छा दृश्य दिखाता है। पलक झपकते ही, आप देखते हैं कि इस क्षेत्र में पक्षियों की सबसे बड़ी संख्या बतख/गीज़/जलपक्षी श्रेणी में है। मिनेसोटा '10,000 झीलों की भूमि' है इसलिए यह आश्चर्य की बात नहीं है!

✅ इस डेटासेट पर कुछ और मायने रखने की कोशिश करें। क्या आपको कुछ आश्चर्य होता है?

## डेटा की तुलना करना

आप नए अक्ष बनाकर समूहीकृत डेटा की विभिन्न तुलनाओं को आज़मा सकते हैं। किसी पक्षी की श्रेणी के आधार पर उसकी अधिकतम लंबाई की तुलना करने का प्रयास करें:

```python
maxlength = birds['MaxLength']
plt.barh(y=birds['Category'], width=maxlength)
plt.rcParams['figure.figsize'] = [6, 12]
plt.show()
```
![डेटा की तुलना करना](images/category-length.png)

यहां कुछ भी आश्चर्य की बात नहीं है: हमिंगबर्ड में पेलिकन या गीज़ की तुलना में कम से कम अधिकतम लंबाई होती है। यह अच्छा है जब डेटा तार्किक समझ में आता है!

आप डेटा को सुपरइम्पोज़ करके बार चार्ट के अधिक दिलचस्प विज़ुअलाइज़ेशन बना सकते हैं। आइए किसी दी गई पक्षी श्रेणी पर न्यूनतम और अधिकतम लंबाई को सुपरइम्पोज़ करें:

```python
minLength = birds['MinLength']
maxLength = birds['MaxLength']
category = birds['Category']

plt.barh(category, maxLength)
plt.barh(category, minLength)

plt.show()
```
इस प्लॉट में आप न्यूनतम लंबाई और अधिकतम लंबाई की प्रति पक्षी श्रेणी की सीमा देख सकते हैं। आप सुरक्षित रूप से कह सकते हैं कि, इस डेटा को देखते हुए, पक्षी जितना बड़ा होगा, उसकी लंबाई सीमा उतनी ही बड़ी होगी। चित्ताकर्षक!

![superimposed values](images/superimposed.png)

## 🚀 चुनौती

यह पक्षी डेटासेट एक विशेष पारिस्थितिकी तंत्र के भीतर विभिन्न प्रकार के पक्षियों के बारे में जानकारी का खजाना प्रदान करता है। इंटरनेट के चारों ओर खोजें और देखें कि क्या आप अन्य पक्षी-उन्मुख डेटासेट पा सकते हैं। उन तथ्यों की खोज करने के लिए इन पक्षियों के चारों ओर चार्ट और ग्राफ़ बनाने का अभ्यास करें जिन्हें आपने महसूस नहीं किया है।
## [व्याख्यान के बाद प्रश्नोत्तरी](https://purple-hill-04aebfb03.1.azurestaticapps.net/quiz/17)

## समीक्षा और स्व अध्ययन

इस पहले पाठ ने आपको मात्राओं की कल्पना करने के लिए Matplotlib का उपयोग करने के तरीके के बारे में कुछ जानकारी दी है। विज़ुअलाइज़ेशन के लिए डेटासेट के साथ काम करने के अन्य तरीकों के बारे में कुछ शोध करें। [प्लॉटली](https://github.com/plotly/plotly.py) प्वह है जिसे हम इन पाठों में शामिल नहीं करेंगे, इसलिए देखें कि यह क्या पेशकश कर सकता है।
## कार्यभार

[लाइन्स, स्कैटर, और बार्स](assignment.md)