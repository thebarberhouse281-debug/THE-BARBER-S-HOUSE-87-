{
  "name": "The Barber’s House 87",
  "short_name": "Barber’s 87",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#000000",
  "theme_color": "#FFD700",
  "description": "Reserva tu cita en The Barber’s House 87",
  "icons": [
    {
      "src": "/icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
self.addEventListener("install", (e) => {
  e.waitUntil(
    caches.open("barbers-house-cache").then((cache) => {
      return cache.addAll(["/", "/index.html", "/manifest.json"]);
    })
  );
});

self.addEventListener("fetch", (e) => {
  e.respondWith(
    caches.match(e.request).then((response) => {
      return response || fetch(e.request);
    })
  );
});import { Html, Head, Main, NextScript } from "next/document";

export default function Document() {
  return (
    <Html lang="es">
      <Head>
        <link rel="manifest" href="/manifest.json" />
        <meta name="theme-color" content="#FFD700" />
      </Head>
      <body>
        <Main />
        <NextScript />
        <script>
          {`if ("serviceWorker" in navigator) {
              navigator.serviceWorker.register("/service-worker.js");
            }`}
        </script>
      </body>
    </Html>
  );
}
