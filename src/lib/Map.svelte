<!-- src/lib/Map.svelte -->
<script>
    import { onMount } from 'svelte';
  
    let L;
    let mapContainer;
  
    onMount(async () => {
      // クライアントサイドでのみLeafletをロード
      const leafletModule = await import('leaflet');
      L = leafletModule.default;
  
      // 地図の初期設定
      const map = L.map(mapContainer).setView([35.41056640163119, 135.3452760149828], 13); // 新しい座標を設定
  
      // OpenStreetMapタイルを追加
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(map);
  
      // カスタムアイコンを作成
      const customIcon = L.icon({
        iconUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-icon.png', // アイコンURL
        iconSize: [25, 41],  // アイコンのサイズ
        iconAnchor: [12, 41], // アイコンのアンカー位置（位置合わせ）
        popupAnchor: [1, -34], // ポップアップのアンカー位置
        shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-shadow.png',  // シャドウ画像
        shadowSize: [41, 41],  // シャドウのサイズ
        shadowAnchor: [12, 41],  // シャドウのアンカー位置
      });
  
      // 新しい座標にマーカーを追加
      L.marker([35.41056640163119, 135.3452760149828], { icon: customIcon }).addTo(map).bindPopup('池内幼稚園');
    });
  </script>
  
  <style>
    #map {
      width: 100%;       /* 幅を100%に設定 */
      height: 400px;     /* 高さを400pxに設定 */
    }
  </style>
  
  <div id="map" bind:this={mapContainer}></div>  <!-- 地図を描画するDOM要素 -->
  