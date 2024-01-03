<!-- Test.svelte -->
<script>
  let selectedTab = ''; // Default selected tab
  let currentQuestionIndex = 0; // Index of the current question
  let userAnswers = []; // User's answers
  let showScore = false; // To show score at the end
  let ready = false; // To show score at the end
  let score = 0; // User's score

  // Sample question structure
  const basicQuestions = [
    
{ question: "Co to jest 'globalne ocieplenie'?", answers: ["a) Zjawisko związane z zimowym ubraniem", "b) Stopniowe podwyższanie się średniej temperatury na Ziemi", "c) Nazwa jednej z planet w Układzie Słonecznym", "d) Metoda uprawy roślin w szklarniach"], correctAnswer: "b) Stopniowe podwyższanie się średniej temperatury na Ziemi" },

{ question: "Jaka jest główna przyczyna topnienia lodowców na świecie?", answers: ["a) Nadmierna ilość deszczu", "b) Emisja gazów cieplarnianych", "c) Wprowadzanie chemikaliów do wód oceanicznych", "d) Wpływ działalności wulkanicznej"], correctAnswer: "b) Emisja gazów cieplarnianych" },

{ question: "Skąd pochodzi większość energii elektrycznej w Polsce?", answers: ["a) Wiatr", "b) Węgiel", "c) Słońce", "d) Gaz ziemny"], correctAnswer: "b) Węgiel" },

{ question: "Co to jest 'recykling'?", answers: ["a) Proces oczyszczania rzek", "b) Ponowne wykorzystywanie surowców z odpadów", "c) Metoda sadzenia drzew w lasach", "d) Oznaczanie obszarów chronionych"], correctAnswer: "b) Ponowne wykorzystywanie surowców z odpadów" },

{ question: "Które zjawisko atmosferyczne jest związane z nadmiernymi opadami deszczu, powodującymi zalania?", answers: ["a) Tornado", "b) Susza", "c) Gradobicie", "d) Powódź"], correctAnswer: "d) Powódź" },

{ question: "Dlaczego topnienie lodowców ma wpływ na poziom mórz i oceanów?", answers: ["a) Zmniejsza ilość wody pitnej na Ziemi", "b) Zwiększa objętość wód oceanicznych", "c) Powoduje przemieszczanie się kontynentów", "d) Sprzyja rozwojowi raf koralowych"], correctAnswer: "b) Zwiększa objętość wód oceanicznych" },

{ question: "Które z miast w Polsce jest najbardziej zanieczyszczone?", answers: ["a) Katowice", "b) Nowa Ruda", "c) Kraków", "d) Warszawa"], correctAnswer: "b) Nowa Ruda" },

{ question: "Czym są opady kwasowe i dlaczego są szkodliwe dla środowiska?", answers: ["a) Deszcze zawierające kwasy, szkodliwe dla gleb", "b) Opady atmosferyczne z kwasami, szkodliwe dla rzek", "c) Opady deszczu zawierające substancje kwasowe, szkodliwe dla roślin i wód", "d) Kwaśne deszcze, korzystne dla rolnictwa"], correctAnswer: "c) Opady deszczu zawierające substancje kwasowe, szkodliwe dla roślin i wód" },

{ question: "Co to jest 'efekt cieplarniany'?", answers: ["a) Zjawisko ogrzewania klimatu przez słońce", "b) Wzrost temperatury w kabinie sauny", "c) Zatrzymywanie ciepła przez atmosferę Ziemi", "d) Nazwa jednej z planet w Układzie Słonecznym"], correctAnswer: "c) Zatrzymywanie ciepła przez atmosferę Ziemi" },

{ question: "Dlaczego ochrona bioróżnorodności jest istotna dla ekosystemów?", answers: ["a) Zwiększa ilość pestycydów w glebie", "b) Chroni przed pożarami lasów", "c) Zapewnia stabilność ekosystemów, utrzymanie równowagi biologicznej", "d) Sprzyja szybszemu wzrostowi populacji gatunków zagrożonych"], correctAnswer: "c) Zapewnia stabilność ekosystemów, utrzymanie równowagi biologicznej" },
    // ... More questions
  ];

  const passionateQuestions = [
    { question: "Jakie konkretnie gazy cieplarniane przyczyniają się do wzrostu efektu cieplarnianego?", answers: ["a) Metan, dwutlenek węgla, podtlenek azotu", "b) Ozon, argon, ksenon", "c) Azot, tlen, dwutlenek siarki", "d) Propan, butan, etanol"], correctAnswer: "a) Metan, dwutlenek węgla, podtlenek azotu" },

    { question: "Jakie zjawisko atmosferyczne może być skutkiem globalnych zmian klimatu?", answers: ["a) Trąba powietrzna", "b) Gradobicie", "c) El Niño", "d) Mgła radiacyjna"], correctAnswer: "c) El Niño" },

    { question: "W jaki sposób działalność człowieka wpływa na zjawisko suszy?", answers: ["a) Zwiększając ilość opadów deszczu", "b) Zanieczyszczając wody gruntowe", "c) Emitując gazów cieplarnianych", "d) Wycinając lasy"], correctAnswer: "d) Wycinając lasy" },

    { question: "Co to jest 'kwas deszczowy' i jakie ma skutki?", answers: ["a) Deszcz zawierający kwasy, korzystny dla rolnictwa", "b) Opady deszczu o niskim pH, szkodliwe dla gleb i wód", "c) Deszcz pochodzący z obszarów przemysłowych, bogaty w minerały", "d) Deszcz o silnym natężeniu, powodujący erozję gleby"], correctAnswer: "b) Opady deszczu o niskim pH, szkodliwe dla gleb i wód" },

    { question: "Dlaczego rozwój rolnictwa ekologicznego jest uważany za korzystny dla środowiska?", answers: ["a) Większa ilość stosowanych pestycydów", "b) Mniejsze zużycie wody", "c) Intensywniejsze stosowanie sztucznych nawozów", "d) Zwiększona emisja gazów cieplarnianych"], correctAnswer: "b) Mniejsze zużycie wody" },

    { question: "Co to jest 'krajobraz kulturowy' i dlaczego jest ważny dla ochrony środowiska?", answers: ["a) Obszar geograficzny o niekorzystnych warunkach atmosferycznych", "b) Formacja geologiczna charakteryzująca się unikalnymi cechami", "c) Obszar, na którym ludzie kształtowali środowisko przez wieki", "d) Specjalnie chroniony obszar przyrodniczy"], correctAnswer: "c) Obszar, na którym ludzie kształtowali środowisko przez wieki" },

    { question: "Które z poniższych zwierząt jest zagrożone wyginięciem w Polsce z powodu utraty naturalnych siedlisk?", answers: ["a) Żubr", "b) Ryś", "c) Kuna leśna", "d) Sarna"], correctAnswer: "b) Ryś" },

    { question: "W wyniku jakiego procesu następuje zakwaszanie wód powierzchniowych, co wpływa na życie organizmów wodnych?", answers: ["a) Emisja CO2", "b) Rozpuszczanie siarki", "c) Wydobycie ropy naftowej", "d) Opady kwasowe"], correctAnswer: "d) Opady kwasowe" },

    { question: "Które z poniższych przedsięwzięć promuje ochronę przyrody i bioróżnorodności w Polsce?", answers: ["a) Wylesianie", "b) Budowa autostrad", "c) Program Natura 2000", "d) Rozwój kopalni"], correctAnswer: "c) Program Natura 2000" },

    { question: "Jakie są główne skutki zanieczyszczenia wód powierzchniowych dla życia organizmów wodnych?", answers: ["a) Zwiększenie ilości tlenu w wodzie", "b) Zagrożenie dla organizmów wodnych przez substancje chemiczne", "c) Poprawa jakości wód", "d) Zwiększenie bioróżnorodności"], correctAnswer: "b) Zagrożenie dla organizmów wodnych przez substancje chemiczne" },

    // ... More questions
  ];

  function selectTab(tab) {
    ready = true;
    selectedTab = tab;
    currentQuestionIndex = 0;
    userAnswers = [];
    showScore = false;
    score = 0;
  }

  function selectAnswer(answer) {
    userAnswers[currentQuestionIndex] = answer;
    if (currentQuestionIndex < getQuestions().length - 1) {
      currentQuestionIndex++;
    } else {
      calculateScore();
      showScore = true;
    }
  }

  function calculateScore() {
    let correctAnswers = getQuestions().map(q => q.correctAnswer);
    score = userAnswers.reduce((acc, answer, index) => acc + (answer === correctAnswers[index] ? 1 : 0), 0);
  }

  function getQuestions() {
    return selectedTab === 'basic' ? basicQuestions : passionateQuestions;
  }
</script>

<style>
  .test-container {
    text-align: center;
    padding: 20px;
  }

  .tab {
    display: inline-block;
    background-color: #00895c;
    padding: 10px 20px;
    margin: 0 10px;
    color: white;
    outline: none;
    border-radius: 15px;
    cursor: pointer;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    transition: 0.3s;
  }

  .tab:focus {
    box-shadow: 0 0 0 2px white, 0 0 0 4px #66db6a;
  }

  .tab:hover {
    box-shadow: 0 16px 32px rgba(0,0,0,0.2);
  }

  .active {
    background-color: #2e9d32;
  }

  .tab-content {
    margin-top: 20px;
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  }

  p {
    color: black;
  }
  #score {
    color: white;
  }
</style>

<div class="test-container">
  {#if !ready}
  <button class="tab {selectedTab === 'basic' ? 'active' : ''}" on:click={() => selectTab('basic')}>Podstawowy</button>
  <button class="tab {selectedTab === 'passionate' ? 'active' : ''}" on:click={() => selectTab('passionate')}>Pasjonat</button>
  {/if}

  {#if ready}
    {#if !showScore}
      <div class="tab-content">
        <p>{getQuestions()[currentQuestionIndex].question}</p>
        {#each getQuestions()[currentQuestionIndex].answers as answer}
          <button on:click={() => selectAnswer(answer)}>{answer}</button>
        {/each}
      </div>
    {:else}
      <div class="score-display">
        <p id="score">Twoj wynik: {score}/{getQuestions().length}</p>
      </div>
    {/if}
  {/if}
</div>
