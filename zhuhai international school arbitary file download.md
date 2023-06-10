zhuhai international school infected with arbitrary file download vulnerabilitie with can cause a huge risks and loses because the attacker can download any file from the server


summary:
  the website uses a wordpress outdated theme that called awake2 in this theme you can download skins
  in ("zischina.com/wp-content/themes/awake2/lib/script/dl-skin.php") dl-skin.php is a php script that makes you download skins that is in the website
  but the script doesn't check if the downloaded skin is a skin or a file from the server
  the attackers can download any files from the server like ../../../etc/passwd which has juicy information
  
  all you need to do is send post request to zischina.com/wp-content/themes/awake2/lib/script/dl-skin.php with the following parameters:
    "_mysite_download_skin": "The file you want to download",
    "submit": "Download"
    
  
  Solutions:
    delete the outdated theme
    
  

![unknown](https://github.com/NoordKing1/Fiverr_portfolio/assets/73787446/b2c61549-33b7-4fd3-a7e5-bbf2d1ddc0dc)
