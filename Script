let standings = {};
teams.forEach(t => standings[t] = { W: 0, D: 0, L: 0, GF: 0, GA: 0, P: 0 });

const team1Select = document.getElementById("team1");
const team2Select = document.getElementById("team2");
teams.forEach(t => {
  team1Select.add(new Option(t, t));
  team2Select.add(new Option(t, t));
});

function playMatch() {
  const team1 = team1Select.value;
  const team2 = team2Select.value;
  if (team1 === team2) {
    alert("Оберіть різні команди!");
    return;
  }

  const score1 = Math.floor(Math.random() * 5);
  const score2 = Math.floor(Math.random() * 5);

  animateGoal(score1 + score2);
  showFans();

  document.getElementById("matchResult").textContent = `${team1} ${score1} : ${score2} ${team2}`;

  updateStandings(team1, team2, score1, score2);
  renderTable();
}

function animateGoal(count) {
  const anim = document.getElementById("goalAnimation");
  anim.innerHTML = "⚽".repeat(count);
  anim.style.animation = "goalEffect 1s infinite";
  setTimeout(() => anim.style.animation = "none", 2000);
}

function showFans() {
  const fans = document.getElementById("fanZone");
  fans.style.display = "block";
  setTimeout(() => fans.style.display = "none", 2000);
}

function updateStandings(t1, t2, s1, s2) {
  standings[t1].GF += s1;
  standings[t1].GA += s2;
  standings[t2].GF += s2;
  standings[t2].GA += s1;

  if (s1 > s2) {
    standings[t1].W++;
    standings[t2].L++;
    standings[t1].P += 3;
  } else if (s1 < s2) {
    standings[t2].W++;
    standings[t1].L++;
    standings[t2].P += 3;
  } else {
    standings[t1].D++;
    standings[t2].D++;
    standings[t1].P++;
    standings[t2].P++;
  }
}

function renderTable() {
  const tbody = document.querySelector("#leagueTable tbody");
  tbody.innerHTML = "";

  const sorted = Object.entries(standings).sort((a, b) => b[1].P - a[1].P);
  sorted.forEach(([team, s]) => {
    const row = document.createElement("tr");
    row.innerHTML = `<td>${team}</td>
      <td>${s.W + s.D + s.L}</td>
      <td>${s.W}</td>
      <td>${s.D}</td>
      <td>${s.L}</td>
      <td>${s.GF}:${s.GA}</td>
      <td>${s.P}</td>`;
    tbody.appendChild(row);
  });
}

function renderCalendar() {
  const list = document.getElementById("calendarList");
  calendar.forEach(match => {
    const li = document.createElement("li");
    li.textContent = `${match.home} vs ${match.away}`;
    list.appendChild(li);
  });
}

renderTable();
renderCalendar();
