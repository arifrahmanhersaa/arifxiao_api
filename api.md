<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Data dengan Jquery 01</title>

   <!-- harus tehubung dengan internet agar Jquery berfungsi, krn CDN -->
   <script src="https://code.jquery.com/jquery-3.5.1.min.js" 
   integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" 
   crossorigin="anonymous"></script>

   <style type="text/css">
      input, button{
         padding:10px;
         margin: 5px
      }
   </style>
</head>
<body>
   <h1>Akses API dengan Jquery ajax</h1>
   <button id="tombol">Load</button><img id="load" src="load.gif">
   <table border="1"></table>
   <script>      
      $().ready(function(){
         $("#load").hide();

         $("#tombol").click(function(){
            //ajax
            $.ajax({
               dataType: "json",
               url: "https://mangamint.kaedenoki.net/api/recommended", 
               beforeSend: function(){//proses sebelum ajax berhasil
                  $("#load").show();
               },
               success: function(result){//berhasil
                     console.log(result);
                     
                     var manga = result.manga_list;

                    var isiTable = "<tr><th>Judul</th><th>Gambar</th></tr>";
                    $.each(JSON.parse(JSON.stringify(manga)), function(key, val){
                     isiTable += "<tr><td>"+val.title+"</td><td><img src='"+ val.thumb+"' loading='lazy' height='200px'></td></tr>";
                  });
                     
                     $("table").append(isiTable);

                     $("#load").hide();
               }
            });   
         });
      });
   </script>
</body>
</html>