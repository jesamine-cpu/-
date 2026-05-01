import React, { useState, useEffect } from 'react';
import { Triangle, Play, RotateCcw, CheckCircle2, XCircle } from 'lucide-react';

// 題庫設計 (根據上傳的圖片內容擷取，敘述中不包含答案關鍵字)
const allQuestions = [
  {
    id: 1,
    scenario: "你在設計講義提問時，刻意設計了一道沒有標準解答的題目，希望刺激學生在課本內容基礎上，發揮更多思考與創造力。",
    correctAnswer: "答案多元",
    options: ["答案多元", "啟動討論", "歸納列舉", "蒐集想法"],
    category: "問題&任務設計",
    color: "bg-[#4d5b87]",
    explanation: "「答案多元」是開放型問題的特性，有豐富可能的答案，能刺激學生在知識點基礎上發揮更多思考與創造力。"
  },
  {
    id: 2,
    scenario: "在進行小組任務時，你沒有站在講台上，而是平和安穩地遊走於各組座位間，觀察學生的狀態，適時進行師生對話。",
    correctAnswer: "教師姿態",
    options: ["引導表達", "表達形式", "教師姿態", "啟動討論"],
    category: "主持引導",
    color: "bg-[#8b181a]",
    explanation: "「教師姿態」是指老師化身為導演兼主持人，平和安穩地遊走於座位間觀察學生行為，並適時引導思考或討論。"
  },
  {
    id: 3,
    scenario: "在學生自由發言時，你專注傾聽他們想說的話，並在引導間穿插自己的觀點，且維持「引導傾聽：老師觀點 ≒ 2：1」的比例。",
    correctAnswer: "引導表達",
    options: ["引導表達", "重述", "推動參與", "尋求回應"],
    category: "主持引導",
    color: "bg-[#8b181a]",
    explanation: "「引導表達」是引導學生說出想法的過程，傾聽學生想法，並在引導間穿插老師觀點（比例約2:1）。"
  },
  {
    id: 4,
    scenario: "除了口語回答之外，你還讓學生透過文字、圖像、音樂甚至上台表演等方式來呈現他們思考的結果。",
    correctAnswer: "表達形式",
    options: ["討論形式", "表達形式", "答案多元", "深入追問"],
    category: "主持引導",
    color: "bg-[#8b181a]",
    explanation: "「表達形式」是設計學生表達的方式，除口語外，可佐以文字、圖像、音樂、表演等，或接龍、咖啡館等變化式。"
  },
  {
    id: 5,
    scenario: "當多位同學同時舉手想發言時，為了讓大家知道都有發言機會且能安心傾聽，你明確指定：『學仔你是1號，阿思你是2號...請學仔先發言。』",
    correctAnswer: "安排順序",
    options: ["安排順序", "蒐集想法", "保留機會", "接納讚美"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「安排順序」是在自由發言且多位學生舉手時，事先安排好表達順序，讓學生安心傾聽他人且知道自己有機會發言。"
  },
  {
    id: 6,
    scenario: "當全班大部分人都同意某種看法時，為了支持少數見解並擴大討論範圍，你問道：『我們已經聽了三種想法，有誰有不同想法嗎？有第四種觀點嗎？』",
    correctAnswer: "平衡觀點",
    options: ["連結主題", "平衡觀點", "排序觀點", "歸納列舉"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「平衡觀點」是接納不同觀點，擴大討論範圍，支持少數見解的學生，讓學生感覺到不論什麼觀點都會被接納。"
  },
  {
    id: 7,
    scenario: "你觀察到某位平時較安靜的學生剛剛眉頭皺了一下，似乎有話想說，於是你溫和地詢問：『你剛剛若有所思，是否正想說點什麼？』",
    correctAnswer: "保留機會",
    options: ["關注交集", "保留機會", "連結主題", "重述"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「保留機會」是留意學生的非語言訊息（如皺眉、若有所思），主動為安靜或思考較慢的學生創造安全的表達機會。"
  },
  {
    id: 8,
    scenario: "為了在討論剛開始時暖場，你帶著鼓勵的話語和姿態問：『有誰有其他想法？舉手～』並自己先舉起手示範，引導大家發言。",
    correctAnswer: "推動參與",
    options: ["排序觀點", "推動參與", "啟動討論", "尋求回應"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「推動參與」是在剛開始進行表達時，為了擴大學生參與，使用鼓勵的話語和姿態（如自己先舉手示範）來引導學生暖場。"
  },
  {
    id: 9,
    scenario: "為了維持討論焦點並擴大參與，當某位同學發表完之後，你沒有馬上接著講課，而是轉向全班問：『對於剛剛的發言內容，有誰想要對他提問嗎？』",
    correctAnswer: "尋求回應",
    options: ["蒐集想法", "教師姿態", "尋求回應", "深入追問"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「尋求回應」是為了擴大參與並維持討論焦點，在一位學生發言後，鼓勵其他學生對該發言內容進行提問或回應。"
  },
  {
    id: 10,
    scenario: "聽到學生特別的想法，你先留意他的非語言訊息，並以簡短的語句搭配語調大聲給予肯定：『太棒了！』或『說得真好！』",
    correctAnswer: "接納讚美",
    options: ["接納讚美", "推動參與", "重述", "引導表達"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「接納讚美」是留意學生的非語言訊息，並以簡短語句搭配語調，大聲給予表達者肯定，接納其感受與觀點。"
  },
  {
    id: 11,
    scenario: "你從學生的表達細節中發現了很有發展性的重點，為了鼓勵他充分表達，你順勢提問：『可否再多說一些？』或『可以舉個例子嗎？』",
    correctAnswer: "深入追問",
    options: ["深入追問", "關注交集", "排序觀點", "蒐集想法"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「深入追問」是從表達細節中發現張力點，進一步追問以協助釐清和探索想法，鼓勵學生充分表達，藉此產生更多學習。"
  },
  {
    id: 12,
    scenario: "你以輕快的節奏請全班發表意見，不論多奇特的想法都先列出來，並善用重述引導學生以較短的句子表達。",
    correctAnswer: "蒐集想法",
    options: ["蒐集想法", "歸納列舉", "討論形式", "答案多元"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「蒐集想法」是以輕快的節奏列出想法，不論多奇特都先列出，並善用重述引導學生以較短句子表達。"
  },
  {
    id: 13,
    scenario: "發問後台下一片安靜，你刻意保持沉默，不急著給提示，放鬆並透過目光和肢體語言將注意力放在全班身上，讓大家有3-5秒的時間消化訊息與準備表達。",
    correctAnswer: "停頓",
    options: ["停頓", "蒐集想法", "保留機會", "安排順序"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「停頓」是刻意暫停、沉默（3-5秒或10-15秒），能協助學生進入思考、消化訊息並做好表達的準備。"
  },
  {
    id: 14,
    scenario: "為了確認自己和全班都有聽懂某位學生的長篇大論，你使用自己的語言換句話說：『聽起來你是說...，對嗎？』來核對對方是否認同。",
    correctAnswer: "重述",
    options: ["深入追問", "重述", "尋求回應", "關注交集"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「重述」是引導學生說出想法的方法之一，老師使用自己的語言換句話說（簡要重述），用以核對對方的意思，維持中立且不帶判斷。"
  },
  {
    id: 15,
    scenario: "當兩派學生提出差異甚大的觀點時，你幫忙歸納差異，並引導大家發現共同目標：『我聽到大家提出不同想法，但大家似乎都在思考如何解決這個問題，這樣對嗎？』",
    correctAnswer: "關注交集",
    options: ["排序觀點", "歸納列舉", "關注交集", "平衡觀點"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「關注交集」是管理多元觀點的技巧，當出現不同想法時，引導學生覺察共通處，歸納差異並聚焦於交集（共同目標）。"
  },
  {
    id: 16,
    scenario: "學生提出了一個意料之外的想法，打破了全班的思考框架，你於是追問他：『你的想法和主題之間的關聯是什麼，請為我們說明一下？』",
    correctAnswer: "連結主題",
    options: ["連結主題", "深入追問", "尋求回應", "重述"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「連結主題」是邀請表達者說明提出的想法與討論主題之間的連結，意料之外的想法常能打破全班思考框架。"
  },
  {
    id: 17,
    scenario: "班上出現兩種不同的想法，你簡要重述後說：『我們接下來將各開放5分鐘時間表達，關於A想法，有誰要回應嗎？』讓兩種想法都能被充分討論。",
    correctAnswer: "排序觀點",
    options: ["排序觀點", "安排順序", "平衡觀點", "蒐集想法"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「排序觀點」是在兩種想法並存時，簡要重述並分別引導討論（如A想法、B想法），讓兩種想法都能被充分討論。"
  },
  {
    id: 18,
    scenario: "大家提出了很多想法，你邀請一位學生將這些想法記錄在黑板上，並說：『現在大家提出來的想法包括某某、某某和某某，這樣對嗎？』讓全班看到每個人的想法。",
    correctAnswer: "歸納列舉",
    options: ["歸納列舉", "蒐集想法", "排序觀點", "表達形式"],
    category: "主持引導",
    color: "bg-[#e88d8d]",
    explanation: "「歸納列舉」是讓學生看到每個人的想法，可由老師或學生主導，並邀請學生紀錄於黑板等顯眼處以聚焦表達。"
  },
  {
    id: 19,
    scenario: "準備進入小組互動前，你考量了效率，向全班說明了目的和時間，並宣布：『請由生日月份最小的人開始說話』。",
    correctAnswer: "啟動討論",
    options: ["啟動討論", "討論形式", "安排順序", "教師姿態"],
    category: "引導討論",
    color: "bg-[#7a187a]",
    explanation: "「啟動討論」是老師引導小組進行討論的開始，需考量效率、說明目的和時間，並決定由誰開始（如隨機順序或生日等）。"
  },
  {
    id: 20,
    scenario: "為了讓每位學生都參與，且保持動能，你在課堂中適時切換了原組分享、分派任務、逛藝廊、拼湊等不同的互動樣貌。",
    correctAnswer: "討論形式",
    options: ["討論形式", "啟動討論", "表達形式", "問題&任務設計"],
    category: "引導討論",
    color: "bg-[#7a187a]",
    explanation: "「討論形式」是小組討論的多種樣貌，透過適時切換形式（如原組討論、分派任務、逛藝廊等），讓每位學生都參與並保持動能。"
  }
];

// 陣列洗牌函數
const shuffleArray = (array) => {
  const shuffled = [...array];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
};

export default function App() {
  const [gameState, setGameState] = useState('start'); // start, playing, result, end
  const [questions, setQuestions] = useState([]);
  const [currentIndex, setCurrentIndex] = useState(0);
  const [score, setScore] = useState(0);
  const [selectedOption, setSelectedOption] = useState(null);
  const [isCorrect, setIsCorrect] = useState(null);
  const [wrongAnswers, setWrongAnswers] = useState([]); // 新增：記錄錯題

  // 初始化遊戲
  const startGame = () => {
    // 按照題庫原始順序出題 (不隨機打亂題目)，但為每題的選項洗牌
    const gameQuestions = allQuestions.map(q => ({
      ...q,
      options: shuffleArray(q.options)
    }));
    // 取全部 10 題
    setQuestions(gameQuestions);
    setCurrentIndex(0);
    setScore(0);
    setGameState('playing');
    setSelectedOption(null);
    setIsCorrect(null);
    setWrongAnswers([]); // 清空錯題紀錄
  };

  // 處理選擇答案
  const handleOptionClick = (option) => {
    if (gameState !== 'playing') return; // 防止重複點擊
    
    setSelectedOption(option);
    const correct = option === questions[currentIndex].correctAnswer;
    setIsCorrect(correct);
    
    if (correct) {
      setScore(score + 1);
    } else {
      // 紀錄錯題與使用者的選擇
      setWrongAnswers(prev => [...prev, {
        question: questions[currentIndex],
        userAnswer: option
      }]);
    }
    
    setGameState('result');
  };

  // 下一題
  const nextQuestion = () => {
    if (currentIndex + 1 < questions.length) {
      setCurrentIndex(currentIndex + 1);
      setGameState('playing');
      setSelectedOption(null);
      setIsCorrect(null);
    } else {
      setGameState('end');
    }
  };

  // 模擬學思達牌卡的 UI 元件
  const ShareStartCard = ({ title, category, onClick, isSelected, isResult, isCorrectAnswer, color }) => {
    let cardClass = "relative bg-white rounded-xl shadow-md border-2 overflow-hidden cursor-pointer transition-all duration-300 transform hover:-translate-y-1 hover:shadow-xl w-full flex flex-col aspect-[2/3] max-h-[300px]";
    
    if (isResult) {
      if (isCorrectAnswer) {
        cardClass += " border-green-500 ring-4 ring-green-200 scale-105 z-10";
      } else if (isSelected && !isCorrectAnswer) {
        cardClass += " border-red-500 opacity-70 grayscale";
      } else {
        cardClass += " border-gray-200 opacity-50";
      }
    } else {
      cardClass += isSelected ? " border-indigo-500 ring-4 ring-indigo-200" : " border-gray-200";
    }

    // 依據類別給予不同顏色頂部
    const topBarColor = color || "bg-[#e88d8d]"; 

    return (
      <div className={cardClass} onClick={onClick}>
        {/* 頂部有三角形的色條 */}
        <div className={`h-1/4 ${topBarColor} relative flex items-center justify-center p-2`}>
          <div className="absolute left-2 bottom-0 w-0 h-0 border-l-[15px] border-l-transparent border-r-[15px] border-r-transparent border-b-[20px] border-b-white"></div>
          <div className="absolute right-2 bottom-0 w-0 h-0 border-l-[15px] border-l-transparent border-r-[15px] border-r-transparent border-b-[20px] border-b-white"></div>
          <h3 className="text-white font-bold text-lg tracking-widest">{category}</h3>
        </div>
        
        {/* 中央圓形 Badge */}
        <div className="absolute top-[25%] left-1/2 transform -translate-x-1/2 -translate-y-1/2 z-10">
          <div className="bg-[#5c595a] text-white rounded-full w-14 h-14 flex items-center justify-center text-sm font-bold shadow-sm leading-tight text-center p-2">
            {title.substring(0, 2)}<br/>{title.length > 2 ? title.substring(2,4) : ''}
          </div>
        </div>

        {/* 底部文字區 */}
        <div className="flex-1 flex items-center justify-center p-4 bg-gray-50 pt-8">
           <p className="text-xl font-bold text-gray-800 text-center tracking-wider">{title}</p>
        </div>

        {/* 結果圖示 */}
        {isResult && isCorrectAnswer && (
          <div className="absolute top-2 right-2 text-green-300 bg-white rounded-full">
            <CheckCircle2 size={24} className="text-green-500" fill="white" />
          </div>
        )}
        {isResult && isSelected && !isCorrectAnswer && (
          <div className="absolute top-2 right-2 text-red-300 bg-white rounded-full">
            <XCircle size={24} className="text-red-500" fill="white" />
          </div>
        )}
      </div>
    );
  };

  return (
    <div className="min-h-screen bg-slate-100 font-sans selection:bg-rose-200">
      {/* 頂部導航 */}
      <header className="bg-white shadow-sm py-4 px-6 flex justify-between items-center sticky top-0 z-50">
        <div className="flex items-center gap-2">
          <div className="w-8 h-8 bg-[#e88d8d] rounded-md flex items-center justify-center shadow-inner">
            <div className="w-0 h-0 border-l-[8px] border-l-transparent border-r-[8px] border-r-transparent border-b-[12px] border-b-white"></div>
          </div>
          <h1 className="text-xl font-bold text-gray-800">學思達牌卡互動挑戰</h1>
        </div>
        {gameState !== 'start' && gameState !== 'end' && (
          <div className="text-sm font-semibold bg-slate-100 py-1 px-3 rounded-full text-slate-600">
            得分: {score} / {questions.length}
          </div>
        )}
      </header>

      <main className="max-w-4xl mx-auto p-6 mt-4">
        {/* 開始畫面 */}
        {gameState === 'start' && (
          <div className="bg-white rounded-2xl shadow-xl p-10 text-center max-w-2xl mx-auto mt-10 border-t-8 border-[#e88d8d]">
            <h2 className="text-3xl font-bold text-gray-800 mb-6">歡迎來到教學現場</h2>
            <p className="text-gray-600 mb-8 text-lg leading-relaxed">
              您是一位正在進行學思達教學的老師。接下來會出現各種「課堂情境」，請根據描述，找出最符合該情境所使用的<span className="font-bold text-[#e88d8d]">主持引導牌卡</span>。
            </p>
            <div className="grid grid-cols-2 gap-4 mb-8 text-left text-sm text-gray-500 bg-slate-50 p-6 rounded-xl">
              <div className="flex items-start gap-2">
                <CheckCircle2 size={18} className="text-green-500 shrink-0 mt-0.5" />
                <span>仔細閱讀情境敘述</span>
              </div>
              <div className="flex items-start gap-2">
                <CheckCircle2 size={18} className="text-green-500 shrink-0 mt-0.5" />
                <span>從 4 張牌卡中選出正確答案</span>
              </div>
              <div className="flex items-start gap-2">
                <CheckCircle2 size={18} className="text-green-500 shrink-0 mt-0.5" />
                <span>共 20 個情境挑戰（依序出現）</span>
              </div>
              <div className="flex items-start gap-2">
                <CheckCircle2 size={18} className="text-green-500 shrink-0 mt-0.5" />
                <span>測試您的教學反應力！</span>
              </div>
            </div>
            <button 
              onClick={startGame}
              className="bg-[#e88d8d] hover:bg-rose-500 text-white font-bold py-3 px-10 rounded-full inline-flex items-center gap-2 transition-transform transform hover:scale-105 shadow-lg"
            >
              <Play fill="currentColor" size={20} />
              開始挑戰
            </button>
          </div>
        )}

        {/* 遊戲與結果畫面 */}
        {(gameState === 'playing' || gameState === 'result') && questions.length > 0 && (
          <div className="space-y-8">
            {/* 情境區 */}
            <div className="bg-white rounded-2xl shadow-lg p-6 md:p-8 border-l-8 border-[#5c595a] relative">
              <div className="absolute -top-4 -left-4 w-10 h-10 bg-slate-800 text-white rounded-full flex items-center justify-center font-bold text-lg shadow-md">
                Q{currentIndex + 1}
              </div>
              <h3 className="text-sm font-bold text-gray-400 mb-2 uppercase tracking-widest">課堂情境觀察</h3>
              <p className="text-xl md:text-2xl text-gray-800 leading-relaxed font-medium">
                {questions[currentIndex].scenario}
              </p>
            </div>

            {/* 牌卡選項區 */}
            <div>
              <h3 className="text-center text-gray-500 font-medium mb-6">請選擇您正在使用的牌卡：</h3>
              <div className="grid grid-cols-2 md:grid-cols-4 gap-4 md:gap-6 px-2 md:px-0">
                {questions[currentIndex].options.map((option, idx) => (
                  <ShareStartCard
                    key={idx}
                    title={option}
                    category={questions[currentIndex].category}
                    color={questions[currentIndex].color}
                    onClick={() => handleOptionClick(option)}
                    isSelected={selectedOption === option}
                    isResult={gameState === 'result'}
                    isCorrectAnswer={option === questions[currentIndex].correctAnswer}
                  />
                ))}
              </div>
            </div>

            {/* 回饋區塊 (僅在選擇後顯示) */}
            {gameState === 'result' && (
              <div className={`p-6 rounded-xl flex flex-col sm:flex-row items-center justify-between shadow-md animate-fade-in ${isCorrect ? 'bg-green-50 border border-green-200' : 'bg-red-50 border border-red-200'}`}>
                <div className="flex items-center gap-4 mb-4 sm:mb-0">
                  {isCorrect ? (
                    <CheckCircle2 size={40} className="text-green-500" />
                  ) : (
                    <XCircle size={40} className="text-red-500" />
                  )}
                  <div>
                    <h4 className={`text-xl font-bold ${isCorrect ? 'text-green-700' : 'text-red-700'}`}>
                      {isCorrect ? '答對了！' : '啊，不太對喔！'}
                    </h4>
                    <p className={`text-sm ${isCorrect ? 'text-green-600' : 'text-red-600'}`}>
                      {isCorrect ? '您精準掌握了這個引導技巧。' : `這題的正確牌卡應該是「${questions[currentIndex].correctAnswer}」。`}
                    </p>
                  </div>
                </div>
                <button 
                  onClick={nextQuestion}
                  className={`font-bold py-3 px-8 rounded-full shadow-sm transition-colors ${
                    isCorrect 
                      ? 'bg-green-600 hover:bg-green-700 text-white' 
                      : 'bg-red-600 hover:bg-red-700 text-white'
                  }`}
                >
                  {currentIndex + 1 === questions.length ? '查看總結' : '下一題'}
                </button>
              </div>
            )}
          </div>
        )}

        {/* 結束畫面 */}
        {gameState === 'end' && (
          <div className="bg-white rounded-2xl shadow-xl p-10 text-center max-w-2xl mx-auto mt-10 border-t-8 border-[#5c595a]">
            <h2 className="text-3xl font-bold text-gray-800 mb-2">挑戰完成！</h2>
            <p className="text-gray-500 mb-8">您已完成所有的情境測驗</p>
            
            <div className="flex justify-center items-center gap-4 mb-8">
              <div className="text-6xl font-black text-[#e88d8d]">
                {score}
              </div>
              <div className="text-2xl text-gray-400 font-bold">/</div>
              <div className="text-4xl font-bold text-gray-600">
                {questions.length}
              </div>
            </div>

            <div className="bg-slate-50 p-6 rounded-xl mb-8">
              <p className="text-lg text-gray-700 font-medium">
                {score === questions.length ? "太厲害了！您簡直是學思達引導大師，對各種牌卡時機瞭若指掌！" : 
                 score >= questions.length / 2 ? "表現不錯！您已經掌握了大部分的引導技巧，再多熟悉一下牌卡會更順手喔！" : 
                 "還需要一點練習！建議可以把實體牌卡拿出來多翻閱幾次，熟悉不同情境的應用。"}
              </p>
            </div>

            {/* 新增：錯題回顧區塊 */}
            {wrongAnswers.length > 0 && (
              <div className="mt-8 mb-8 text-left animate-fade-in">
                <h3 className="text-2xl font-bold text-gray-800 mb-6 border-b-2 border-slate-200 pb-3 flex items-center gap-2">
                  <RotateCcw size={24} className="text-[#e88d8d]" />
                  錯題回顧與解析
                </h3>
                <div className="space-y-6">
                  {wrongAnswers.map((item, idx) => (
                    <div key={idx} className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm relative overflow-hidden">
                      {/* 左側裝飾線條 */}
                      <div className="absolute top-0 left-0 w-1.5 h-full bg-[#e88d8d]"></div>
                      
                      <p className="font-medium text-gray-800 mb-4 text-lg leading-relaxed">
                        <span className="text-[#e88d8d] font-bold text-sm bg-rose-50 px-2 py-1 rounded mr-3 inline-block transform -translate-y-0.5">情境 {item.question.id}</span>
                        {item.question.scenario}
                      </p>
                      
                      <div className="flex flex-col sm:flex-row gap-4 mb-4 text-sm font-medium">
                        <div className="flex items-center gap-2 text-red-600 bg-red-50 px-3 py-2 rounded-lg border border-red-100 flex-1">
                          <XCircle size={18} className="shrink-0" /> 您選擇了：{item.userAnswer}
                        </div>
                        <div className="flex items-center gap-2 text-green-600 bg-green-50 px-3 py-2 rounded-lg border border-green-100 flex-1">
                          <CheckCircle2 size={18} className="shrink-0" /> 正確牌卡：{item.question.correctAnswer}
                        </div>
                      </div>
                      
                      <div className="text-sm text-slate-700 bg-slate-50 p-4 rounded-lg border border-slate-100 leading-relaxed">
                        <span className="font-bold text-slate-800 mr-1 block mb-1">💡 牌卡解析：</span>
                        {item.question.explanation}
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            )}

            <button 
              onClick={startGame}
              className="bg-slate-800 hover:bg-slate-900 text-white font-bold py-3 px-10 rounded-full inline-flex items-center gap-2 transition-transform transform hover:scale-105 shadow-lg"
            >
              <RotateCcw size={20} />
              再玩一次
            </button>
          </div>
        )}
      </main>

      {/* 簡單的自定義動畫 */}
      <style dangerouslySetInnerHTML={{__html: `
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(10px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
          animation: fadeIn 0.4s ease-out forwards;
        }
      `}} />
    </div>
  );
}
