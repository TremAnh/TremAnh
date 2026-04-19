<div align="center">
<img src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExcGIweHFxeGwwa3Iyd29odnExaG12OWMyMjZpaXI2ZGJsc3Uwa29xNyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/tXwHTbQuyjo1q/giphy.gif" align="center" style="width: 100%" />
</div>  
  
meo tram~
// Authorization token that must have been created previously. See : https://developer.spotify.com/documentation/web-api/concepts/authorization
const token = 'BQARtUKj9hx-Q-7nd7vbp3QgW2tpZSzOAJotNP8Dy8QaBigYfu6K3fpxTXF0Nuinjr6KcTTuzPFPcwSfsXp5NW-p4maShBABHw994UxeLlV17ylFpraaU_TEUThjI005SOPv_UwAhm8vZAJiSUHwjwxexB9K-qr0WWXJL3DsHMQ6AN4-ormwE-mvecUhBRwweDzIz3cbTQVzTqheOY4wmjnh12XAnvd3uFOoeliNdZ4TR6Jc_caqk9UzgDu_DJ_O-84niVKf_ryUG_reAixdc8u3M-z4RcgObxGa0P6ZLJMME5N9M8HbgwOgq_KeLGlTo7PhwQ';
async function fetchWebApi(endpoint, method, body) {
  const res = await fetch(`https://api.spotify.com/${endpoint}`, {
    headers: {
      Authorization: `Bearer ${token}`,
    },
    method,
    body:JSON.stringify(body)
  });
  return await res.json();
}

async function getTopTracks(){
  // Endpoint reference : https://developer.spotify.com/documentation/web-api/reference/get-users-top-artists-and-tracks
  return (await fetchWebApi(
    'v1/me/top/tracks?time_range=long_term&limit=5', 'GET'
  )).items;
}

const topTracks = await getTopTracks();
console.log(
  topTracks?.map(
    ({name, artists}) =>
      `${name} by ${artists.map(artist => artist.name).join(', ')}`
  )
);
