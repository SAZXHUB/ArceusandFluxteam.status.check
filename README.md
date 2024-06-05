<html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>Status Updater</title><style>html, body{width: 100%; height: 100%; margin: 0; font-family: Arial, sans-serif; color: white; text-align: center; background-size: cover; background-repeat: no-repeat; background-attachment: fixed; display: flex; flex-direction: column; justify-content: center; align-items: center;}#status{font-size: 3em; margin-top: 20px; display: flex; flex-direction: row; align-items: center; justify-content: center;}.online{color: lightgreen;}.offline{color: red;}.button{margin-top: 20px; padding: 10px 20px; background-color: #4CAF50; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 1em;}</style></head><body><h1>Status Updater</h1><div id="status">Checking status for: spdmteam.com</div><button class="button" onclick="checkStatus('spdmteam.com', 'https://i.postimg.cc/3rPvbDhY/Mobile-Image-7a84dac27ba539ba6cf9.webp')">Check spdmteam.com Status</button><button class="button" onclick="checkStatus('flux.li', 'https://i.postimg.cc/yYLz80Nz/Screenshot-2024-0605-215849.jpg')">Check flux.li Status</button><button class="button" onclick="showLogs()">Show Logs</button><script>let logs=JSON.parse(localStorage.getItem('logs')) || [];function updateStatus(message){const statusDiv=document.getElementById('status'); statusDiv.textContent=message;}function checkStatus(website, background){updateStatus("Checking status for: " + website); document.body.style.backgroundImage="url('" + background + "')"; const startTime=Date.now(); fetch('https://' + website,{mode: 'no-cors'}) .then(response=>{const statusDiv=document.getElementById('status'); if (response.ok || response.type==='opaque'){updateStatus(website + " is online"); statusDiv.className='online'; const endTime=Date.now(); const downtime=(endTime - startTime) / 1000; logs.push({website, status: 'online', downtime}); localStorage.setItem('logs', JSON.stringify(logs));}else{updateStatus(website + " is offline"); statusDiv.className='offline'; logs.push({website, status: 'offline'}); localStorage.setItem('logs', JSON.stringify(logs));}console.log(logs);}) .catch(error=>{console.error('Error fetching status:', error); updateStatus(website + " is offline"); const statusDiv=document.getElementById('status'); statusDiv.className='offline'; logs.push({website, status: 'offline'}); localStorage.setItem('logs', JSON.stringify(logs)); console.log(logs);});}function showLogs(){let logsText=""; if (logs.length > 0){logs.forEach((log, index)=>{logsText +="Log " + (index + 1) + ": " + log.website + " - Status: " + log.status; if (log.status==="offline"){logsText +=" - Downtime: " + log.downtime + " seconds";}logsText +="\n";});}else{logsText="No logs available.";}alert(logsText);}function goBack(){window.history.back();}setInterval(()=>{checkStatus('spdmteam.com', 'https://i.postimg.cc/3rPvbDhY/Mobile-Image-7a84dac27ba539ba6cf9.webp'); checkStatus('flux.li', 'https://i.postimg.cc/yYLz80Nz/Screenshot-2024-0605-215849.jpg');}, 5000);</script></body></html>
