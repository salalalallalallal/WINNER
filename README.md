<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>축구 경기 결과</title>
    <style>
        body {
            text-align: center;
            font-size: 2rem;
            margin-top: 20%;
            font-family: Arial, sans-serif;
        }
    </style>
</head>
<body>
    <p id="message">🔮 오늘의 축구 경기 결과는? 🔮</p>
    <button onclick="fetchSoccerResults()">눌러서 확인하기</button>

    <script>
        async function fetchSoccerResults() {
            try {
                // 축구 경기 API 엔드포인트로 변경 (여기서는 예시로 EPL 데이터를 사용한다고 가정)
                const response = await fetch('https://api.sportsdata.io/v3/soccer/scores/json/GamesByDate/2024-MAR-18?key=YOUR_API_KEY');
                const games = await response.json();
                
                if (games.length === 0) {
                    document.getElementById("message").innerText = "오늘 경기 결과가 없습니다.";
                    return;
                }

                let resultText = "오늘의 축구 경기 결과:\n";
                games.forEach(game => {
                    resultText += `${game.HomeTeam.Name} ${game.HomeTeamScore} - ${game.AwayTeam.Name} ${game.AwayTeamScore}\n`;
                });

                // 결과 메시지 업데이트
                document.getElementById("message").innerText = resultText;
            } catch (error) {
                document.getElementById("message").innerText = "데이터를 불러오는 데 문제가 발생했습니다.";
            }
        }
    </script>
</body>
</html>
