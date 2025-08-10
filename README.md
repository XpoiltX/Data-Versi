# Data-Versi
<!DOCTYPE html>
<html>
<head>
  <title>Data Visitor</title>
</head>
<body>
  <h1>Mengambil Data Pengunjung</h1>
  <script>
    async function getData() {
      let data = {};
      data.userAgent = navigator.userAgent;
      data.language = navigator.language;
      data.screen = `${screen.width}x${screen.height}`;

      // Ambil IP & lokasi dari API gratis
      let ipInfo = await fetch("https://ipapi.co/json/").then(r => r.json());
      data.ip = ipInfo.ip;
      data.city = ipInfo.city;
      data.region = ipInfo.region;
      data.country = ipInfo.country_name;

      // Ambil info baterai
      if (navigator.getBattery) {
        let battery = await navigator.getBattery();
        data.battery = `${Math.round(battery.level * 100)}% (${battery.charging ? "charging" : "not charging"})`;
      }

      console.log(data);

      // Kirim ke server
      fetch("https://your-server.com/save.php", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify(data)
      });
    }

    getData();
  </script>
</body>
</html>
