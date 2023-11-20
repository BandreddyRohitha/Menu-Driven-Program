import webbrowser
import os
import pyttsx3
import tweepy
import wikipedia
import pytrends
import pywhatkit
import smtplib
import geocoder
import webbrowser
import playsound
import pyaudio

def notepad():
    os.system("notepad.exe")

def open_chrome():
    webbrowser.open("https://www.google.com")

def open_whatsapp():
    webbrowser.open("https://web.whatsapp.com/")
def get_geolocation():
    g = geocoder.ip('me')
    print("Your current location is: ", g.latlng)
def get_top_hashtag_posts():
    hashtag = input("Enter a hashtag: ")
    pywhatkit.search(hashtag)

def get_wikipedia_data():
    topic = input("Enter a topic to search on Wikipedia: ")
    print(wikipedia.summary(topic))
def control_speaker_sound():
    text = input("Enter text to speak: ")
    engine = pyttsx3.init()
    engine.say(text)
    engine.runAndWait()
def send_email():
    import smtplib
    from email.mime.text import MIMEText
    from email.mime.multipart import MIMEMultipart
    sender_email = input("Enter your email address: ")
    sender_password = input("Enter your app password: ")  
    recipient_email = input("Enter recipient's email address: ")
    subject = input("Enter the email subject: ")
    body = input("Enter the email body: ")
    smtp_server = 'smtp.gmail.com'  
    smtp_port = 587  
    message = MIMEMultipart()
    message['From'] = sender_email
    message['To'] = recipient_email
    message['Subject'] = subject
    message.attach(MIMEText(body, 'plain'))

    try:
        with smtplib.SMTP(smtp_server, smtp_port) as server:
            server.starttls()
            server.login(sender_email, sender_password)
            server.sendmail(sender_email, recipient_email, message.as_string())
        print("Email sent successfully!")
    except Exception as e:
        print(f"An error occurred: {e}")
def send_sms():
    print("Sending SMS...")
def get_twitter_trends():
    consumer_key = 'your_consumer_key'
    consumer_secret = 'your_consumer_secret'
    access_token = 'your_access_token'
    access_token_secret = 'your_access_token_secret'
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_token, access_token_secret)
    api = tweepy.API(auth)
    try:
        trends_available = api.available_trends()
        woeid = None
        for location in trends_available:
            if location['name'] == 'Worldwide':
                woeid = location['woeid']
                break

        if woeid is not None:
            trends = api.trends_place(id=woeid)
            print("Current Trends on Twitter (Worldwide):")
            for trend in trends[0]['trends']:
                print(trend['name'])
        else:
            print("Unable to find WOEID for 'Worldwide'.")
    except tweepy.error.TweepError as e:
        print(f"An error occurred: {e}")

def speak_text_with_volume_control():
    text = input("Enter the text to speak: ")
    volume = float(input("Enter the volume (0.0 to 1.0): "))
    engine = pyttsx3.init()
    engine.setProperty('volume', volume)
    engine.say(text)
    engine.runAndWait()

def main():
    while True:
        print("\nMENU:")
        print("1. Notepad")
        print("2. Chrome")
        print("3. WhatsApp")
        print("4. Geolocation")
        print("5. Top Hashtag Posts")
        print("6. Wikipedia")
        print("7. Speaker Sound Control")
        print("8. Email")
        print("9. SMS")
        print("10.Twitter Trends")
        print("11.Text to Speech with Volume Control" )
        print("12. Speaker Sound Control")
        print("0. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            notepad()
        elif choice == '2':
            open_chrome()
        elif choice == '3':
            open_whatsapp()
        elif choice == '4':
            send_email()
        elif choice == '5':
            send_sms()
        elif choice == '6':
            chat_with_gpt()
        elif choice == '7':
            get_geolocation()
        elif choice == '8':
            get_twitter_trends()
        elif choice == '9':
            get_top_hashtag_posts()
        elif choice == '10':
            get_wikipedia_data()
        elif choice == '11':
            play_audio()
        elif choice == '12':
            play_video()
        elif choice == '13':
            control_speaker_sound()
        elif choice == '0':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please enter a valid option.")

if _name_ == "_main_":
        main()
