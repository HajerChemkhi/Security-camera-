import smtplib,ssl  
from picamera import PiCamera  
from time import sleep  
from email.mime.multipart import MIMEMultipart  
from email.mime.base import MIMEBase  
from email.mime.text import MIMEText  
from email.utils import formatdate  
from email import encoders  
import picamera
import time
import RPi.GPIO as GPIO
import time
from time import sleep

GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)

trig = 2
echo = 3

GPIO.setup(trig,GPIO.OUT)
GPIO.setup(echo,GPIO.IN)

#camera = PiCamera()  
  
#camera.start_preview()  
#sleep(5)  
#camera.capture('testshot.jpg')     # image path set
#sleep(5)  
#camera.stop_preview()  
while(True):

  print( "satrt mesurement...")

  GPIO.output(trig,0)
  GPIO.output(trig,1)
  time.sleep(0.00001)
  GPIO.output(trig,0)

  while GPIO.input(echo) == 0:
     pass
  start = time.time()

  while GPIO.input(echo) == 1:
    pass
  stop=time.time()
  distance = (stop-start)*17000
  print (distance,'cm' )
  time.sleep(0.5)
   
  toaddr = '@gmail.com'      # To id 
  me = '@gmail.com'          # your id
  subject = "What's News"              # Subject
  
  msg = MIMEMultipart()  
  msg['Subject'] = subject  
  msg['From'] = me  
  msg['To'] = toaddr  
  msg.preamble = "test "   
    #msg.attach(MIMEText(text)) 
  if distance <10: 
    camera = picamera.PiCamera()
    camera.capture('testshot.jpg')

    part = MIMEBase('application', "octet-stream")  
    part.set_payload(open("testshot.jpg", "rb").read())  
    encoders.encode_base64(part)  
    part.add_header('Content-Disposition', 'attachment; filename="testshot.jpg"')   # File name and format name
    msg.attach(part)  
   
    try:  
       s = smtplib.SMTP('smtp.gmail.com', 587)  # Protocol
       s.ehlo()  
       s.starttls()  
       s.ehlo()  
       s.login(user = '', password = '')  # User id & password
       #s.send_message(msg)  
       s.sendmail(me, toaddr, msg.as_string())  
       s.quit()  
    #except:  
    #   print ("Error: unable to send email")    
    except smtplib.SMTPException:  
          print ("Error")    
