import re
import requests
from bs4 import BeautifulSoup
import os

#-----<<<<<<-Baidu function body->>>>>>>-----------------
def baidu(keyword, img_limit = 10): 
  folder_name = '{} Baidu download'.format(keyword)
  cur_dir = os.path.join(os.getcwd(), folder_name)
  if not os.path.exists(cur_dir):
    os.mkdir(cur_dir)

  valid_img_count = 0
  error_count = 0

  url = 'https://image.baidu.com/search/flip?tn=baiduimage&ie=utf-8&word='+keyword+'&ct=201326592&v=flip'
  result = requests.get(url)
  html = result.text
  search_result_img = re.findall('"objURL":"(.*?)",',html,re.S)

  for i, img_link in enumerate(search_result_img, start=1):
    if img_limit == valid_img_count:
      break

    separator = img_link.rfind(r'.')            
    file_type = img_link[separator:]            
    if len(file_type) >=6:
      file_type = '.jpg'
    print(file_type)

    try:
      headers = {'User-Agent': 'Mozilla/5.0'}
      req_link = requests.get(img_link, headers=headers)

      img_name = (f'Img_baidu{i:03}{file_type}')
      with open(os.path.join(cur_dir, img_name), 'wb') as f:
        f.write(req_link.content)
      valid_img_count +=1
    except:
      print('Baidu download error')
      error_count += 1
  print(f'Baidu image downloaded: {valid_img_count}')
  print(f'Baidu Error count: {error_count}')
#---------------Baidu function End-----------------------
# baidu('bus', 15)

###-------<<<<<<-Google function body->>>>>>>--------------
def google(keyword, img_limit = 10):
  
#--------------Create folder for images--------------------  
  folder_name = '{} Google download'.format(keyword)
  cur_dir = os.path.join(os.getcwd(), folder_name)
  if not os.path.exists(cur_dir):
    os.mkdir(cur_dir)
#-------------------------------------------------------

# --------Create folder when use home computer-------------
# folder_name = '{} Baidu download'.format(keyword)
# home_dir = os.path.join('D:\Python download', folder_name)
# if not os.path.exists(home_dir):
#   os.mkdir(home_dir)
# -------------------------------------------------------

#---------Preset variable and make soup-----------------
  valid_img_count = 0
  error_count = 0

  search_result = 'https://www.google.com/search?q=' + keyword + '&client=opera&hs=cTQ&source=lnms&tbm=isch&sa=X&ved=0ahUKEwig3LOx4PzKAhWGFywKHZyZAAgQ_AUIBygB&biw=1920&bih=982'
  result_text = requests.get(search_result).text
  soup = BeautifulSoup(result_text, 'html.parser')
#-------------------------------------------------------

##----Loop over soup result and download imgs------------
  try: 
    for i, link in enumerate(soup.find_all('img')):
      if img_limit == valid_img_count:
       break 
      file_link_src = link.get('src')

#-----------For some image link without http://-----------
      img_link_head = []
      if str(file_link_src)[0:5] == 'http:':
        img_link_head = ''
      elif str(file_link_src)[0:5] == "https":
        img_link_head = ''
      else:
        img_link_head = 'https:'
      file_link = img_link_head + str(file_link_src)
#-----------------------------------------------------

#---To find the file type and change strange ending to JPG---
      separator = file_link.rfind(r'.')            
      file_type = file_link[separator:]            
      if len(file_type) >=6:
        file_type = '.jpg'
      print(file_type)
#-----------------------------------------------------

#------Request file thought link and download images--------
      headers = {'User-Agent': 'Mozilla/5.0'}
      req_link = requests.get(file_link, headers=headers)
      img_name = (f'Img{i:03}{file_type}')

      with open(os.path.join(cur_dir, img_name), 'wb') as f:
        f.write(req_link.content)
#-------------------------------------------------------     
      valid_img_count += 1
  except:
    print('Error occure')
    error_count += 1
##------------------------------------------------------
  print(f'Google images downloaded: {valid_img_count}')
  print(f'Error occurance: {error_count}')
###-----------Google function End-----------------------
# google('bus',12)  

if __name__ == '__main__':
  print('Please insert keyword:')
  key_word = input()
  print('Please insert search limit:')
  search_limit = input()
  baidu(key_word, int(search_limit))
  google(key_word,int(search_limit))
