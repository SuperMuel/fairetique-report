---
title: Analysis of Fraud Facilitated by Fairtiq in Occitanie and Nouvelle-Aquitaine: Reflections on Consequences and Possible Solutions
author: MALLET Samuel
date: April 1, 2023
---

# Abstract
In 2021, SNCF launched a collaboration with the mobile application Fairtiq in the Occitanie and Nouvelle-Aquitaine regions. This initiative allows eligible travelers to use their smartphones to travel by TER train simply by pressing a button, and the billing of the trip is automatic. However, the ticket displayed by the application does not contain a QR code or any other means of certification, thus opening the door to numerous potential fraud methods.

In this document, we explore several ticket forgery techniques, including a concrete example of an application. We also examine how malicious individuals could exploit these vulnerabilities for profit, notably through various scams.

![Fairtiq Close Up](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/fairtiq_close_up_FR.jpg)

# Introduction
I am a student pursuing a double degree in mathematics and computer science at the University of Sciences in Montpellier. For a long time, I wanted to learn how to code applications and websites, and it was in 2021 that I started this learning journey. My goal is to develop applications for various devices, which is why I am interested in cross-platform frameworks. I undertake a few personal projects to practice until one day an SNCF employee introduced me to the Fairtiq application and its benefits. This application allows users to bypass train ticket reservations and travel with just a button press.

During my first use, I noticed that the ticket was not secure and that it would be easy to make a copy. Indeed, any web or mobile developer could create an application or website that allows configuring and displaying a fake ticket. As for me, I was looking for a simple mobile application project to sharpen my skills. I then set out to create a fake application. I just needed to copy the ticket interface and add a form to input the personal information required for ticket display. I entered my name, surname, date of birth, and departure station (Figure 1), and voilà! I had created a ticket valid on the entire TER network in Occitanie, perfectly identical to the original and could be presented to controllers (Figure 2). All of this was accomplished within an hour of discovering Fairtiq.


## Figures 1 and 2: Configuration and Ticket Pages

<div style="display: flex; justify-content: space-around;">
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/first_version/ticket_creation.jpg" alt="Configuration page. Contains fields for first name, surname, departure city, date of birth, and ticket activation date and time." width="95%">
    <p>Figure 1: Configuration Page</p>
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/first_version/ticket_page.jpg" alt="Ticket page" width="95%">
    <p>Figure 2: Ticket Page</p>
  </div>
</div>


### First Version of the Fake Application

Is it really that simple? I wondered. At that moment, I was unaware of the age of the application and considered the lack of a QR code as a voluntary omission due to the system's youth. The flaw would be fixed quickly, I thought.

I then set aside "Fairetique" (the name I had given to the fake application) until the day a controller conducted an unusual check of my ticket. (Of course, I was using Fairtiq, the original application; otherwise, I wouldn't be writing this but would likely be in prison.) My phone resting on the table in front of me, he turned it towards him, left the ticket screen to return to the application menu, and then displayed the ticket again. If I had used my fake application, the deception would have been discovered because the main menu was nothing other than the ticket configuration page (Figure 1). This manipulation confirmed to me that I was certainly not the only one who had "discovered" this flaw and apparently, some were taking advantage of it.

I decided to create a new version of my application, capable of addressing almost any eventuality and defrauding on all TER trains without limitation.

For external readers, I will start with a brief introduction to Fairtiq. Next, I will present some fraud methods based on the absence of a QR code, then I will demonstrate my fake application. Finally, I will conclude with a study of the potential consequences of this flaw.

---

> **Warning:**
>
> This document is written for educational and informational purposes only. The author neither promotes nor encourages fraud or any other illegal activity. The examples and methods described herein are intended to raise awareness among readers about the potential risks associated with the absence of a QR code on train tickets and to encourage improvements in ticketing system security. Under no circumstances shall the author be held responsible for the misuse of the information contained in this document.

---

# What is Fairtiq?

Fairtiq is a smartphone application that simplifies the purchase of tickets for public transport. [The brand's website](https://fairtiq.com/fr) states: "With one gesture, obtain the right ticket, always at the best price."

## Usage
The principle of Fairtiq is simple: after configuring the application, it geolocates the user. When detected at a train station, the user simply has to swipe the "start" button to begin the journey (Figure 3).

Thanks to the smartphone's GPS, the application automatically determines the route taken by the user.

At the end of the trip, the user simply has to press the same button again to end the journey (Figure 4). The journey is then calculated and billed automatically to the user.

## Figures 3 and 4: Starting the Ticket

<div style="display: flex; justify-content: space-around;">
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/start_button.png" alt="Ticket not started. The page contains an illustration and a button to swipe to start the ticket." width="95%">
    <p>Figure 3: Ticket Not Started</p>
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/stop_button.jpg" alt="Started ticket. The page contains a button to display the ticket, as well as the button to swipe to stop it. A timer shows the activation time of the ticket." width="95%">
    <p>Figure 4: Started Ticket</p>
  </div>
</div>


## The Ticket
During a check, the traveler displays their ticket using the "Show My Ticket" button visible in Figure 4.

This ticket contains:
- A timer indicating the time elapsed since the ticket was activated, allowing verification that the traveler did not activate it just before the controller arrived.
- The departure station or stop.
- The name and date of birth of the traveler.
- Additional information specific to the transport company.

One might expect this ticket to also include a QR code, which is indeed the case for some transport companies in Switzerland and Germany (Figure 5). Moreover, when downloading Fairtiq from the App Store and Play Store, one of the illustrative images shows a ticket containing a QR code (Figure 6).

## Figures 5 and 6: Tickets with QR Codes

<div style="display: flex; justify-content: space-around;">
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/billet_avec_qr_1.jpg" alt="Source: Play Store" width="95%">
    <p>Figure 5: Source: Play Store</p>
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/billet_avec_qr_2.jpg" alt="Source: stwab.de" width="95%">
    <p>Figure 6: Source: stwab.de</p>
  </div>
</div>

## Fairtiq and SNCF
Since 2016, Fairtiq has gradually established itself in Switzerland, Liechtenstein, Austria, Germany, and Belgium (in that order) (Figure 7). In 2021, Fairtiq arrived in France in partnership with SNCF and in the Occitanie and Nouvelle-Aquitaine regions. These regions promise a simplified user experience as well as a reduction in travel costs for all TER trains.

## Figure 7: Validity Range of Fairtiq
![Validity Range of Fairtiq](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/rayon_validite_fairtiq.png)

### Fairtiq in Occitanie
#### For Young People:
Launched in April 2021, the "+=0" offer in Occitanie was initially tested on a panel of 2000 young people aged 18 to 26. It was in September that it became available to all young people in this age group. This offer allows them to pay no more than 50% of the ticket price, or even travel for free depending on the number of trips made. The details of the offer described in Figure 8 indicate that a traveler making at least 15 round trips per month can travel for free. Conversely, if this traveler is less regular and makes fewer than 15 round trips per month, they travel for free starting from the 11th trip, but will have to pay part or all of their first 10 trips of the following month.

## Figure 8: The +=0 Offer from the Occitanie Region
![The +=0 Offer from the Occitanie Region](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/offres/occitanie/plus_eq_zero.jpg)

Recently, it was announced that, starting in September 2023, this scheme would be extended to young people from the age of 16 and to regular lines of the liO coach network for those aged 18-26.

#### For Seniors:
Targeted at people aged 60 and over, the "+=-" offer appeared more than a year after the previous offer, providing discounts ranging from -10% to -50%, detailed in Figure 9.

## Figure 9: The +=- Offer from the Occitanie Region
![The +=- Offer from the Occitanie Region](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/offres/occitanie/plus_egal_moins/reductions.jpg)

Both young people and seniors benefit from all "liO" trains in Occitanie, covering over 30 lines and 280 stations (Figure 10).

## Figure 10: The Regional Rail Network of Occitanie
![The Regional Rail Network of Occitanie](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/offres/occitanie/reseau_ferroviaire_occitanie.png)

### Fairtiq in Nouvelle-Aquitaine
Similarly, the Nouvelle-Aquitaine region has implemented an offer for its TER services using the Fairtiq application. Named "FlexTER", it was initially reserved for those under 28 but has been accessible to all since April 2022.

Unlike the offers in Occitanie, the discounts applied are not specific to Fairtiq but depend on other regional offers and subscriptions. Billing calculations are performed weekly and determine the most advantageous offer for the traveler.

This ensures that users will not pay more for their trips through Fairtiq than if they had subscribed to a subscription on their own, and all of this is without commitment. Users can travel across the entire TER network in Nouvelle-Aquitaine, represented in Figure 11.

## Figure 11: The Regional Rail Network of Nouvelle-Aquitaine
![The Regional Rail Network of Nouvelle-Aquitaine](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/offres/nouvelle-aquitaine/carte_reseau.png)

### Interregional Travel
As previously discussed, Fairtiq is available for both young people and seniors in both Occitanie and Nouvelle-Aquitaine. But is it possible to travel between regions seamlessly?

It is interesting to note that certain stations located in Nouvelle-Aquitaine, such as those in Pau, Agen, and Brive-la-Gaillarde, are accessible from the Occitan network. This is visible on the map in Figure 10. Once at one of these stations, the user simply needs to open the Fairtiq application and change the active region (Figure 12) to continue their journey throughout Nouvelle-Aquitaine. Although this method may take a bit longer, it is possible to make a trip like Perpignan-Poitiers (and vice versa) using only the TER and the Fairtiq application.

## Figure 12: Changing the Region in Fairtiq
![Changing the Region in Fairtiq](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/changement_regions/changement_illustration.png)

# New Fraud Methods
*From now on, we will refer to Fairtiq only for use in the Occitanie and Nouvelle-Aquitaine regions.*

Although this application greatly simplifies ticket purchasing, it paves the way for new fraud methods. Already, nothing prevents a traveler on a train journey from stopping their ticket just after a check, in order to end their trip for free.

However, Fairtiq could continue to analyze the user's behavior after stopping the ticket to detect this manipulation. To guard against this, a user could turn off the smartphone's GPS and completely close Fairtiq to prevent it from functioning in the background. In this way, Fairtiq would not be able to determine whether the user continued their journey on the train after stopping the ticket.

It should be noted that a similar method exists using conventional ticketing applications, although this is more challenging. For example, a traveler making a direct trip from Toulouse to Montpellier could initially book a ticket from Toulouse to Carcassonne. If they are not checked during this first part, they then buy a ticket from Carcassonne to Montpellier. This can be done particularly through the SNCF Connect application, which allows users to book TER tickets just minutes before departure from the relevant station. Assuming the user has a 50% chance of being checked during the first part of their journey, they have a 50% chance of halving the cost of their journey. On average, this results in a 25% reduction in the total trip costs.

Due to the ability to stop their journey at any time while traveling with Fairtiq, it is much easier and more effective to carry out this manipulation with this application. This drawback is therefore caused by one of the application's greatest advantages, and it seems difficult to overcome.

On the other hand, the following methods exploit the lack of certification of the Fairtiq ticket, which is limited to displaying the date, time, name, and date of birth of the user, as well as the boarding station. It is therefore impossible to verify the authenticity of a ticket without additional information. It is indeed enough to imitate the ticket, as the following sections describe in detail.

## Screenshot of the Ticket
Since it is now very easy to take a video capture of the smartphone screen, a user who frequently takes the same trip may be tempted to record a video of their ticket during part or all of their journey. Thus, during their next trips, they could present the video to the controller.

However, this technique is not foolproof, as each ticket incorporates the date and time of the trip. Since this information is relatively small, the individual might hope it goes unnoticed. Additionally, they could decrease the font size on their smartphone to make the ticket harder to read.

## Video Editing
To address the date issue, an individual with basic video editing skills could easily modify the date on the screenshot before their trip. By also changing the text indicating the departure station as well as the timer, it would be possible to generate a video of a ticket for any trip. It is not difficult to imagine that the process could be automated, or at least accelerated, making it possible to generate a ticket just before each trip.

However, although this seems rare, the controller could ask to see other elements of the application if deemed necessary. For example, they might ask to leave the ticket page to return to the application home screen, as I described in the introduction. This inconvenience can be avoided by creating an almost perfect copy of the application.

# An Example of a Fake Application
In this section, I present an example of an application that allows displaying a fake ticket while perfectly imitating the Fairtiq interface.

In addition to needing to meet the challenges already addressed, the application must also be user-friendly, as we consider it could be made public. This specification will be useful in section 14.

## First Use
Upon the first opening of the application, the user is presented with a brief introduction to Fairtiq and "Fairetique" (Figure 13). It is indeed essential that the user is informed about the normal functioning of Fairtiq.

While the slogan "Travel, Pay No More" lacks originality, it perfectly describes what the user should expect. However, the application warns the user of the illegality of their act and requires them to check a box (Figure 14).

## Figures 13 and 14: First Opening of the Fake Application and Functioning of Fairtiq

<div style="display: flex; justify-content: space-around;">
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/intro/slogan.jpg" alt="First opening of the fake application" width="95%">
    <p>Figure 13: First Opening of the Fake Application</p>
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/intro/tuto_fairtiq_sliding.jpg" alt="Functioning of Fairtiq" width="95%">
    <p>Figure 14: Functioning of Fairtiq</p>
  </div>
</div>


After this brief introduction, the application asks the user to enter their name, surname, and date of birth (Figure 15). This information will be necessary for displaying the ticket.

Next, the user is prompted to authorize (or not) the use of GPS and is then redirected to the home page.

Finally, once the configuration is complete, the application can be used indistinguishably from the original application.

When the user opens the application, they are automatically geolocated, and the nearest station is selected as the departure station. The user can then start and display the ticket (Figure 16).

## Figures 15 and 16: Configuration and Home Page

<div style="display: flex; justify-content: space-around;">
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/user_profile_creation.jpg" alt="Configuration. The user is asked to enter their first name, last name, and date of birth to display on the ticket." width="95%">
    <p>Figure 15: Configuration</p>
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/fake_homepage.jpg" alt="Home page, exactly similar to the real Fairtiq home page." width="95%">
    <p>Figure 16: Home Page</p>
  </div>
</div>


## Activating a Fake Ticket
The ticket is started exactly as shown in Figure 3. Then, even if the application is closed, or the device runs out of battery, the ticket will still remain active upon reopening (except in certain cases; see section 12).

The user can then display their fake ticket (Figure 17).

## Figure 17: Generating the Ticket
![Generating the Ticket](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/ticket_generation/ticket_generation.png)

If the application does not have access to GPS, or if it is disabled, the warning displayed is identical to the original (Figure 18).

<div style="flex: 1; text-align: center;">
<img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/no-gps/acces_restreint_position.jpg" alt="Warning: GPS unavailable" width="55%">
<p>Figure 18: Warning: GPS Unavailable</p>
</div>


We will see later that it is possible to bypass this alert if the user still wishes to use the application without GPS.

## The God Mode
Now that it is possible to generate a fake ticket, some problems remain to be solved.

First, consider the case of an individual who uses the fake application and realizes once on the train that they forgot to activate their ticket. They then immediately activate their ticket, which is always possible even when far from a station. The problem arises when several minutes have passed without the train stopping at a station, and the ticket claims it has been activated for only a few minutes. A controller could detect a problem since the original Fairtiq application prevents the activation of the ticket between two stations. Additionally, a controller might suspect the traveler is attempting to commit fraud by activating their ticket just before the check.

Worse still, the application could locate the user at the next station if it is the nearest station. One might think to calculate the user's direction of travel and ensure the departure station is one from which they are moving away. While this would work in the scenario described above, a user who activates their ticket while driving to their departure station will be located at the nearest station behind them, which is undesirable.

Finally, if the GPS is disabled or unavailable, it will then be impossible to locate the departure station.

It becomes necessary to implement a means to change the activation time of the ticket, as well as the departure station. That is why we introduce the **God Mode**.

## Figure 19: Opening the God Mode
![Opening the God Mode](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/mode_dieu/ouverture_mode_dieu.png)

This hidden menu opens with a long press on the Fairtiq logo on the home page (Figure 19). Designed not to open accidentally, it automatically closes upon reopening the application to make it usable in front of a controller. All kinds of configurations then become possible, and the main ones are reviewed below.

### Changing the Departure Station
At any time, the user can change their departure station: by searching among a long list or using the search bar (Figure 20). It is also possible to let the application display the nearest stations (Figure 21).

This protects the user from any GPS issues, and it then becomes possible to restore their departure station in the event of a location error (e.g., when activating the ticket late).

## Figure 20: Modifying the Departure Station
![Modifying the Departure Station](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/mode_dieu/edit_station/edit_station.jpg)

## Figure 21: Modifying the Departure Station
![Modifying the Departure Station](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/mode_dieu/edit_station/edit_station_geo.jpg)

### Changing the Activation Time of the Ticket
In cases where the user activates their ticket late, as well as in numerous other similar situations, the user has the option to modify the activation time to match a legitimate situation. They can choose a new activation time or simply add or subtract time from the ticket's duration (Figure 22).

Moreover, this date is always stored in the smartphone's permanent memory, and therefore there is no delay when the application is closed or the phone is turned off.

## Figure 22: Modifying the Ticket
![Modifying the Ticket](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/mode_dieu/votre_billet/votre_billet.jpg)

### Automatic Ticket Deactivation
In the official application, the user must manually signal their departure from the train so that the application can stop the ticket in time. However, it is also possible to activate the "Smart Stop" feature, which handles this operation automatically. However, with our fraudulent application, it is easy to forget to deactivate the ticket, which can pose problems during future trips. For example, upon opening the application, the previous ticket may still be active, which poses a risk in the event of a check during boarding.

To avoid this, the fraudulent application allows the user to configure an expiration delay, after which the ticket is automatically deactivated (Figure 23).

## Figure 23: Automatic Ticket Stop Parameter
![Automatic Ticket Stop Parameter](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/mode_dieu/auto_stop.jpg)

### Usage without GPS
As previously discussed (Figure 18), a warning is displayed when GPS is unavailable. In this case, it is not possible to start the ticket unless accessing the God Mode. The user is given the choice not to display this warning, which will change the texts indicating the departure station to loading icons (Figure 24). The user will then be free to select it manually via the God Mode.

## Figure 24: GPS Alert Parameter
![GPS Alert Parameter](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/no-gps/discard_alert.jpg)

### Guiding the User
After installation and once the user has provided the necessary information for the ticket, a message is displayed indicating how to access the God Mode. The user can choose to immediately ignore this message and launch a ticket or follow the instructions to open the hidden menu.

When the menu is first opened, the application guides the user in exploring all the hidden features. This guidance should be completed within a minute. Three examples are illustrated in Figure 25.

## Figure 25: Presentation of the God Mode to the User

<div style="display: flex; justify-content: space-around;">
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/guidage_mode_dieu/open_god_mode.jpg" alt="Presentation of the God Mode to the User" width="95%">
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/guidage_mode_dieu/welcome_god_mode.jpg" alt="Presentation of the God Mode to the User" width="95%">
  </div>
  <div style="flex: 1; text-align: center;">
    <img src="https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/guidage_mode_dieu/departure_station.jpg" alt="Presentation of the God Mode to the User" width="95%">
  </div>
</div>

# Technical Details
## Access to the Application
This application is entirely developed using the Flutter framework. Flutter is an open-source UI software development kit (SDK) created by Google. It is used to develop applications for Android, iOS, Linux, Mac, Windows, Google Fuchsia, and the web from a single codebase.

Thus, the application can be exported for Android and iOS devices, as well as for web browsers.

While it can be easily installed and shared on Android via an .apk file, this is more difficult for Apple devices. Indeed, the brand makes it impossible, or very difficult, to install unknown applications without going through the official "App Store". Thus, one solution would be to host the application on a web server to make it accessible from a browser. This can be done locally: by connecting your computer to the same Wi-Fi network as your smartphone - for example, through a hotspot initiated on the mobile device - and then hosting the application on the computer. The process can be very quick once configured, and it is then sufficient to access the phone's browser at the correct address (typically localhost:80).

Aside from the dependency on a computer or the internet, using the application through a browser does not have a significant impact. In fact, most devices offer the option to add a shortcut to a website on the home screen, which in our case will add a "Fairtiq" icon to the home screen, indistinguishable from an official installation. Furthermore, when opening the application via this shortcut, users benefit from a full-screen interface.

## The System for Detecting the Nearest Station
SNCF has committed to opening up a number of its data. Thus, it is straightforward to retrieve information about the stations in the network.

Following a data preprocessing step using a Python script, I exported the names of the stations and their GPS coordinates to the application. Then, as soon as the user's position is detected, the distance between them and each station is calculated, and the nearest one is selected. All of this is performed directly on the user's phone without any additional verification needed. It is not then difficult to detect the departure station more quickly than the original application, likely because the latter must perform numerous checks. I am particularly thinking of detecting the use of a fake location application, which I have not been able to bypass.

# What Consequences?
I do not believe I have accomplished anything complex by developing this application. On the contrary, I am convinced that I am not the only one who has had this idea, nor the only one capable of creating something similar. Indeed, there are many frameworks to rapidly develop mobile applications, as well as online services that circumvent the need for programming skills. One might also consider the latest advancements in artificial intelligence, which are entirely capable of programming a similar system.

It is evident that any system displaying a fake ticket must closely imitate Fairtiq and thus take the form of an application. Given that it has never been easier to develop an application, I assume that other people are capable of doing what I have presented so far, but better, or rather worse.

In this section, I present methods that individuals could develop to profit, going beyond the initial goal of simply avoiding paying for their own trips.

## Selling the Application
The first idea that comes to mind to make money from what I have already created would be to sell the application to interested individuals.

It would be possible to post ads on social media and then send the application to interested parties in exchange for a sum of money. I particularly think of Snapchat, which has often been a favored platform for drug traffickers.

By setting the price at a multiple of the average cost of a trip, it could be very profitable for many users. The purchase would be recouped within a few trips, and users would be guaranteed to travel for free until the flaw is fixed.

It is easy to share the application with Android users: just send an .apk file. However, this could trigger a snowball effect: given that it is a file, any customer could share it with friends, who in turn could share it again, and so on. This uncontrolled peer-to-peer sharing would then be impossible to stop.

But we can guard against this uncontrollable sharing by customizing the application specifically for each customer. They will receive an application whose ticket displays their name, surname, and date of birth, without being able to modify them. It then becomes unnecessary to share the application, except of course with their twin.

A subscription system then seems like a good solution.

## Usage-based or Subscription Billing System
We could adapt the application to integrate a user authentication and billing system.

Various plans could be imagined, such as "1€ = 1 hour of ticket" or "Unlimited Train for 10€/month".

Unlike the previous method, sharing the application would no longer pose a problem in this case. Compatibility with Apple devices could be ensured by hosting the application on a website.

The main challenge would then be to implement a secure billing system. It would obviously not be wise for the "seller" to implement such a system using their own personal information. Cryptocurrencies therefore emerge as a viable option for transactions between clients and sellers.

## Scams
The ideas mentioned previously rely on exploiting some individuals' willingness to commit fraud. However, I think some actors could take advantage of the vulnerability of honest people. For example, ads for the application or the site could be disseminated on social media, targeting people unfamiliar with Fairtiq. By promising them a radical simplification of their way of traveling (exactly what Fairtiq aims to do), they could be lured into downloading a counterfeit version of Fairtiq. The latter could seek to collect as much personal data as possible, including banking details.

The trick of this technique lies in the difficulty of detecting the counterfeit, since from the user's point of view, the application works. If even a controller cannot identify any anomaly during normal use, how could the user do so? Knowing this, it would even be possible to charge the customer the normal price of the ticket! Given some users' transport budgets, it would not take many victims or much time to accumulate a significant amount of money.

It would also be feasible to distribute the application by promising free tickets. Victims would be offered the first three or four trips for free, enough to ensure they are checked at least once and therefore believe they are using an official application. Once trust is gained, the application could invent any creative excuse to obtain the user's banking details. In doing so, the scammers would also solve a problem: in the previous paragraph, I mentioned the possibility of charging tickets in cryptocurrencies. However, this payment method is not feasible here, since the aim is to pass for an official application. Nonetheless, by promising the application's free usage and still collecting banking details, scammers could use this information in illicit networks and thus make profits. Furthermore, since the application works and allows the person to travel, it could be difficult for the victim to determine the source of their banking details leak.

# What Solutions?
After examining various more or less probable consequences related to the absence of a QR code, one might wonder if there are solutions.

But isn't it tautological? Wouldn't the solution to the absence of a QR code be... the implementation of a QR code?

A partial measure could involve preventing screenshots of the ticket screen, thereby making it more difficult to share tickets among users. However, this does not constitute a definitive solution.

Lacking all the information on SNCF and Fairtiq's strategy, I will formulate several hypotheses that may answer the following question:
## Why does the Fairtiq ticket not contain a QR code on the SNCF network?
### Hypothesis 1: Implementation costs outweigh potential benefits
I am aware that any modification of an application incurs a cost, but I do not know either the complexity or cost associated with modifying an application used on such a large scale, nor the SNCF ticket control infrastructure.

So, I can only note that in 2019, 70,000 travelers used the TER services in Nouvelle-Aquitaine daily, while Fairtiq users in Occitanie amounted to 30,000 young people in May 2022, with an aim of 10,000 users over 60 in 2023.

With such a number of users, I fear that the spread of an application similar to my example would quickly become widespread, and that the share of fraud would become a significant element surpassing the cost of implementing the QR code.

### Hypothesis 2: A ticket without a QR code is easier to use
I am not convinced by this hypothesis. On the one hand, adding a QR code would have no impact on the user experience. On the other hand, the absence of a QR code does not correspond to what is observed elsewhere: as shown in Figure 5, the Fairtiq ticket is presented as having a QR code. Other ticket booking applications, such as SNCF Connect, have one, just like event tickets such as cinema tickets, concert tickets, football match tickets, etc. I believe the public has now become accustomed to QR codes due to the Covid-19 pandemic, which has popularized them, potentially creating confusion among some users.

## Figure 26: Comments Related to the Absence of a QR Code (App Store)
![Comments Related to the Absence of a QR Code](https://raw.githubusercontent.com/SuperMuel/fairetique-report/main/illustrations/images/comments/all3.png)

### Hypothesis 3: The current system is sufficient
In this case, I fear the emergence of scams exploiting this flaw, as described in the previous section.

Moreover, as fraud methods proliferate, I also fear a certain frustration among honest users, who would not understand why they should pay for their tickets while others are profiting from an unaddressed flaw.

### Hypothesis 4: The implementation of the QR code is underway
If this hypothesis holds true, then all the fraud methods previously described will become obsolete, as well as the analysis presented in this document.

# Conclusion
Throughout this study, I examined several fraud methods, including the example of the application I developed. Although this could be improved—especially by allowing manual modification of the ticket text as well as implementing other application menus like the travel history—it presents several advantages. Indeed, the application requires neither account creation nor payment method addition and works without internet access. It also demonstrates greater flexibility in case of error and can sometimes be faster than the original.

Regarding the analysis of consequences and solutions, it is important to note that it is based solely on the elements I currently have at my disposal, and that final conclusions must be drawn by SNCF and Fairtiq. Nevertheless, I hope this analysis can contribute in some way to improving the services offered.

I would also like to note that during my tests, I was unable to fool the application's location system using a fake position application. When I tried to artificially modify my GPS position, the application immediately displayed a loading screen that seemed endless, suggesting that it detects this manipulation.

Finally, I want to apologize if my remarks give the impression that I consider myself an expert in this field. My goal is simply to share my experience and current understanding of the technology, while remaining aware of the complexity of software development. I am open to any opportunity to learn more about the technologies used by SNCF and Fairtiq.

# References

1. **Fairtiq**. *FAIRTIQ celebrates its five years with its partners*. April 28, 2021. [fairtiq.com](https://fairtiq.com/fr/blog/fairtiq-fete-ses-cinq-ans-avec-les-partenaires).

2. **lio.laregion.fr**. *Free liO trains for young people: I travel +, I pay 0 €!* August 23, 2022. [lio.laregion.fr](https://lio.laregion.fr).

3. **laregion.fr**. *A new agreement for more trains, safer and more punctual*. March 23, 2023. [laregion.fr](https://laregion.fr).

4. **ter.sncf.com**. *+ I travel - I pay with +=-*. July 11, 2022. [ter.sncf.com](https://ter.sncf.com).

5. **Wikipedia**. *TER Occitanie*. Last consulted on March 31, 2023. [wikipedia.org](https://fr.wikipedia.org/wiki/TER_Occitanie).

6. **actu.fr**. *SNCF extends its FlexTER application to all of Nouvelle-Aquitaine*. April 1, 2022. [actu.fr](https://actu.fr/nouvelle-aquitaine/angouleme_16015/charente-la-sncf-etend-son-application-flexter-a-toute-la-nouvelle-aquitaine_49839972.html).

7. **ter.sncf.com**. *The FlexTER application*. Last consulted on March 31, 2023. [ter.sncf.com](https://www.ter.sncf.com/nouvelle-aquitaine/flexter).

8. **20min.ch**. *Paying less for the train: "20 minutes" did the test*. March 19, 2018. [20min.ch](https://www.20min.ch/fr/story/payer-le-train-moins-cher-20-minutes-a-fait-le-test-668725504870).

9. **ressources.data.sncf**. *Database of passenger stations*. [ressources.data.sncf](https://ressources.data.sncf.com/explore/dataset/referentiel-gares-voyageurs).

10. **SNCF Nouvelle-Aquitaine**. *Corporate Social Responsibility*, 2019.

11. **laregion.fr**. *With « +=- », seniors will prefer liO trains*. July 11, 2022. [laregion.fr](https://www.laregion.fr/Avec-les-seniors-prefereront-les-liO-trains).

