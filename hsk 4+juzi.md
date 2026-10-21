<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HSK 4 级词汇智能复习闪卡 (全469词带例句版)</title>
    <style>
        :root {
            --primary-color: #4f46e5;
            --primary-hover: #4338ca;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --accent-red: #ef4444;
            --accent-green: #22c55e;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        header {
            text-align: center;
            margin-bottom: 16px;
        }

        header h1 {
            margin: 0 0 6px 0;
            color: var(--primary-color);
            font-size: 1.6rem;
        }

        header p {
            margin: 0;
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .container {
            width: 100%;
            max-width: 520px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .progress-bar {
            width: 100%;
            background-color: #e2e8f0;
            border-radius: 9999px;
            height: 8px;
            overflow: hidden;
            margin-bottom: 16px;
        }

        .progress-fill {
            background-color: var(--primary-color);
            height: 100%;
            width: 0%;
            transition: width 0.3s ease;
        }

        .stats {
            display: flex;
            justify-content: space-between;
            width: 100%;
            margin-bottom: 10px;
            font-size: 0.85rem;
            color: var(--text-muted);
            font-weight: 500;
        }

        /* 闪卡 3D 容器 */
        .flashcard-container {
            perspective: 1000px;
            width: 100%;
            height: 360px;
            margin-bottom: 20px;
            cursor: pointer;
        }

        .flashcard {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s;
            transform-style: preserve-3d;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.05);
            border-radius: 16px;
        }

        .flashcard.flipped {
            transform: rotateY(180deg);
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background-color: var(--card-bg);
            border-radius: 16px;
            border: 1px solid #e2e8f0;
            padding: 20px;
            box-sizing: border-box;
        }

        .card-front {
            font-size: 3.5rem;
            font-weight: bold;
            color: var(--text-main);
        }

        .card-front .hint {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-top: 15px;
            font-weight: normal;
        }

        .card-back {
            transform: rotateY(180deg);
            justify-content: space-between;
        }

        .word-header {
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .pinyin {
            font-size: 1.5rem;
            color: var(--primary-color);
            margin-bottom: 4px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .meaning {
            font-size: 1.1rem;
            color: var(--text-main);
            font-weight: 500;
        }

        /* 例句模块 */
        .example-section {
            width: 100%;
            background-color: #f8fafc;
            border-radius: 12px;
            padding: 12px;
            box-sizing: border-box;
            text-align: left;
            border: 1px dashed #cbd5e1;
            margin-top: 10px;
        }

        .example-title {
            font-size: 0.75rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 4px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .example-hanzi {
            font-size: 1.05rem;
            color: var(--text-main);
            font-weight: 600;
            margin-bottom: 2px;
        }

        .example-pinyin {
            font-size: 0.85rem;
            color: var(--primary-color);
            margin-bottom: 4px;
        }

        .example-trans {
            font-size: 0.8rem;
            color: var(--text-muted);
            font-style: italic;
        }

        /* 语音按钮样式 */
        .audio-btn {
            background: #e0e7ff;
            border: none;
            color: var(--primary-color);
            cursor: pointer;
            font-size: 0.9rem;
            padding: 4px 8px;
            border-radius: 6px;
            transition: all 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 4px;
        }

        .audio-btn:hover {
            background-color: var(--primary-color);
            color: #ffffff;
        }

        /* 控制区 */
        .controls {
            display: flex;
            gap: 12px;
            width: 100%;
            margin-bottom: 16px;
        }

        .btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 12px;
            font-size: 0.95rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
        }

        .btn-dont-know {
            background-color: #fee2e2;
            color: var(--accent-red);
        }
        .btn-dont-know:hover {
            background-color: #fecaca;
        }

        .btn-know {
            background-color: #dcfce7;
            color: var(--accent-green);
        }
        .btn-know:hover {
            background-color: #bbf7d0;
        }

        .nav-controls {
            display: flex;
            justify-content: space-between;
            width: 100%;
            margin-bottom: 24px;
        }

        .btn-nav {
            background-color: #e2e8f0;
            color: var(--text-main);
            padding: 8px 14px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-size: 0.85rem;
        }
        .btn-nav:hover {
            background-color: #cbd5e1;
        }

        /* 错词本区域 */
        .wrong-section {
            width: 100%;
            background: #ffffff;
            border-radius: 16px;
            border: 1px solid #e2e8f0;
            padding: 16px;
            box-sizing: border-box;
        }

        .wrong-section h3 {
            margin-top: 0;
            color: var(--accent-red);
            font-size: 1rem;
            border-bottom: 1px solid #f1f5f9;
            padding-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .wrong-list {
            list-style: none;
            padding: 0;
            margin: 0;
            max-height: 200px;
            overflow-y: auto;
        }

        .wrong-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 10px;
            border-bottom: 1px solid #f8fafc;
            font-size: 0.88rem;
        }

        .wrong-item:hover {
            background-color: #f8fafc;
        }

        .wrong-item span {
            cursor: pointer;
        }

        .remove-wrong {
            background: none;
            border: none;
            color: var(--text-muted);
            cursor: pointer;
            font-size: 0.8rem;
        }
        .remove-wrong:hover {
            color: var(--accent-red);
        }

        .empty-tip {
            color: var(--text-muted);
            text-align: center;
            font-size: 0.85rem;
            padding: 12px 0;
        }
    </style>
</head>
<body>

    <header>
        <h1>HSK 4 级词汇自测闪卡</h1>
        <p>全量 469 词，含带调拼音、印尼语释义与例句发音</p>
    </header>

    <div class="container">
        <div class="stats">
            <span id="counter">词语 1 / 469</span>
            <span>HSK 4 全量词汇</span>
        </div>
        <div class="progress-bar">
            <div class="progress-fill" id="progress"></div>
        </div>

        <!-- 闪卡主体 -->
        <div class="flashcard-container" onclick="flipCard()">
            <div class="flashcard" id="card">
                <!-- 正面 -->
                <div class="card-face card-front">
                    <span id="card-hanzi">阴</span>
                    <div class="hint">点击卡片翻转查看详情</div>
                </div>
                <!-- 背面 -->
                <div class="card-face card-back">
                    <div class="word-header">
                        <div class="pinyin">
                            <span id="card-pinyin">yīn</span>
                            <button class="audio-btn" onclick="event.stopPropagation(); playWordAudio()" title="播放词语发音">🔊 读词</button>
                        </div>
                        <div class="meaning" id="card-meaning">mendung</div>
                    </div>

                    <!-- 例句部分 -->
                    <div class="example-section">
                        <div class="example-title">
                            <span>📝 例句 Example</span>
                            <button class="audio-btn" style="padding: 2px 6px; font-size: 0.75rem;" onclick="event.stopPropagation(); playExampleAudio()" title="播放例句发音">🔊 读例句</button>
                        </div>
                        <div class="example-hanzi" id="card-ex-hanzi">今天天气是阴天。</div>
                        <div class="example-pinyin" id="card-ex-pinyin">Jīntiān tiānqì shì yīntiān.</div>
                        <div class="example-trans" id="card-ex-trans">Today's weather is cloudy.</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 自测操作按钮 -->
        <div class="controls">
            <button class="btn btn-dont-know" onclick="markWrong()">❌ 不会</button>
            <button class="btn btn-know" onclick="markCorrect()">✔️ 认识</button>
        </div>

        <!-- 导航按钮 -->
        <div class="nav-controls">
            <button class="btn-nav" onclick="prevCard()">⬅️ 上一个</button>
            <button class="btn-nav" onclick="nextCard()">下一个 ➡️</button>
        </div>

        <!-- 错词本展示区 -->
        <div class="wrong-section">
            <h3>
                <span>📌 我的错词本 (“不会”的词)</span>
                <span id="wrong-count" style="font-size: 0.8rem; color: var(--text-muted);">0 个词</span>
            </h3>
            <ul class="wrong-list" id="wrongList">
                <div class="empty-tip">暂无错词，继续加油！💪</div>
            </ul>
        </div>
    </div>

    <script>
        // 469个完整的 HSK 4级词汇全量数据库（带例句、带调拼音、英译）
        const vocabData = [
            { hanzi: "阴", pinyin: "yīn", meaning: "mendung", exHanzi: "今天天气是阴天。", exPinyin: "Jīntiān tiānqì shì yīntiān.", exTrans: "Today's weather is cloudy." },
            { hanzi: "运动", pinyin: "yùndòng", meaning: "olahraga", exHanzi: "我每天早上都去运动。", exPinyin: "Wǒ měitiān zǎoshang dōu qù yùndòng.", exTrans: "I go to exercise every morning." },
            { hanzi: "丈夫", pinyin: "zhàngfu", meaning: "suami", exHanzi: "她的丈夫是一位医生。", exPinyin: "Tā de zhàngfu shì yí wèi yīshēng.", exTrans: "Her husband is a doctor." },
            { hanzi: "着", pinyin: "zhe", meaning: "sedang", exHanzi: "门开着呢，请进。", exPinyin: "Mén kāi zhe ne, qǐng jìn.", exTrans: "The door is open, please come in." },
            { hanzi: "矮", pinyin: "ǎi", meaning: "pendek", exHanzi: "弟弟比哥哥矮一点儿。", exPinyin: "Dìdi bǐ gēge ǎi yìdiǎnr.", exTrans: "The younger brother is a bit shorter than the elder brother." },
            { hanzi: "搬", pinyin: "bān", meaning: "pindah", exHanzi: "我们下周要搬家。", exPinyin: "Wǒmen xiàzhōu yào bānjiā.", exTrans: "We are moving next week." },
            { hanzi: "办公室", pinyin: "bàngōngshì", meaning: "kantor", exHanzi: "经理正在办公室开会。", exPinyin: "Jīnglǐ zhèngzài bàngōngshì kāihuì.", exTrans: "The manager is in the office having a meeting." },
            { hanzi: "半", pinyin: "bàn", meaning: "separuh", exHanzi: "现在是三点半。", exPinyin: "Xiànzài shì sāndiǎn bàn.", exTrans: "It is half past three now." },
            { hanzi: "帮忙", pinyin: "bāngmáng", meaning: "membantu", exHanzi: "谢谢你帮我的忙。", exPinyin: "Xièxie nǐ bāng wǒ de máng.", exTrans: "Thank you for helping me." },
            { hanzi: "包", pinyin: "bāo", meaning: "tas", exHanzi: "我的书包里有很多书。", exPinyin: "Wǒ de shūbāo lǐ yǒu hěn duō shū.", exTrans: "There are many books in my bag." },
            { hanzi: "抱", pinyin: "bào", meaning: "hug", exHanzi: "妈妈抱了抱可爱的孩子。", exPinyin: "Māma bào le bào kě'ài de háizi.", exTrans: "The mother hugged the cute child." },
            { hanzi: "饱", pinyin: "bǎo", meaning: "kenyang", exHanzi: "我已经吃饱了。", exPinyin: "Wǒ yǐjīng chī bǎo le.", exTrans: "I am already full." },
            { hanzi: "鼻子", pinyin: "bízi", meaning: "hidung", exHanzi: "大象的鼻子很长。", exPinyin: "Dàxiàng de bízi hěn cháng.", exTrans: "An elephant's trunk is very long." },
            { hanzi: "笔记本", pinyin: "bǐjìběn", meaning: "notebooks", exHanzi: "我买了一台新笔记本电脑。", exPinyin: "Wǒ mǎi le yì tái xīn bǐjìběn diànnǎo.", exTrans: "I bought a new laptop." },
            { hanzi: "变化", pinyin: "biànhuà", meaning: "variasi/perubahan", exHanzi: "这座城市的变化很大。", exPinyin: "Zhè zuò chéngshì de biànhuà hěn dà.", exTrans: "This city has changed a lot." },
            { hanzi: "宾馆", pinyin: "bīnguǎn", meaning: "hotel", exHanzi: "我们就住在前面的宾馆。", exPinyin: "Wǒmen jiù zhù zài qiánmiàn de bīnguǎn.", exTrans: "We are staying at the hotel ahead." },
            { hanzi: "冰箱", pinyin: "bīngxiāng", meaning: "kulkas", exHanzi: "牛奶在冰箱里。", exPinyin: "Niúnǎi zài bīngxiāng lǐ.", exTrans: "The milk is in the refrigerator." },
            { hanzi: "层", pinyin: "céng", meaning: "lantai", exHanzi: "我们住在五层。", exPinyin: "Wǒmen zhù zài wǔ céng.", exTrans: "We live on the fifth floor." },
            { hanzi: "差", pinyin: "chà", meaning: "jelek", exHanzi: "我这次考得太差了。", exPinyin: "Wǒ zhè cì kǎo de tài chà le.", exTrans: "I did very poorly in the exam this time." },
            { hanzi: "衬衫", pinyin: "chènshān", meaning: "kemeja", exHanzi: "他穿了一件白色的衬衫。", exPinyin: "Tā chuān le yí jiàn báisè de chènshān.", exTrans: "He is wearing a white shirt." },
            { hanzi: "船", pinyin: "chuán", meaning: "kapal", exHanzi: "我们坐船去那个小岛。", exPinyin: "Wǒmen zuò chuán qù nàge xiǎodǎo.", exTrans: "We took a boat to that island." },
            { hanzi: "聪明", pinyin: "cōngmíng", meaning: "pintar", exHanzi: "这个孩子非常聪明。", exPinyin: "Zhège háizi fēicháng cōngmíng.", exTrans: "This child is very smart." },
            { hanzi: "打扫", pinyin: "dǎsǎo", meaning: "menyapa", exHanzi: "请把房间打扫干净。", exPinyin: "Qǐng bǎ fángjiān dǎsǎo gānjìng.", exTrans: "Please clean the room thoroughly." },
            { hanzi: "打算", pinyin: "dǎsuàn", meaning: "rencana", exHanzi: "假期你有什么打算？", exPinyin: "Jiàqī nǐ yǒu shénme dǎsuàn?", exTrans: "What are your plans for the holiday?" },
            { hanzi: "打折", pinyin: "dǎzhé", meaning: "diskon", exHanzi: "这家商场正在打折。", exPinyin: "Zhè jiā shāngchǎng zhèngzài dǎzhé.", exTrans: "This mall is currently offering discounts." },
            { hanzi: "担心", pinyin: "dānxīn", meaning: "khawatir", exHanzi: "别担心，一切都会好的。", exPinyin: "Bié dānxīn, yíqiè dōu huì hǎo de.", exTrans: "Don't worry, everything will be fine." },
            { hanzi: "小心", pinyin: "xiǎoxīn", meaning: "hati-hati", exHanzi: "路上有冰，小心一点。", exPinyin: "Lùshang yǒu bīng, xiǎoxīn yìdiǎnr.", exTrans: "There is ice on the road, be careful." },
            { hanzi: "放心", pinyin: "fàngxīn", meaning: "tenang", exHanzi: "请放心，我会按时完成。", exPinyin: "Qǐng fàngxīn, wǒ huì ànshí wánchéng.", exTrans: "Rest assured, I will finish it on time." },
            { hanzi: "开心", pinyin: "kāixīn", meaning: "senang", exHanzi: "今天能见到你真的很开心。", exPinyin: "Jīntiān néng jiàndào nǐ zhēn de hěn kāixīn.", exTrans: "I am really happy to see you today." },
            { hanzi: "伤心", pinyin: "shāngxīn", meaning: "sedih", exHanzi: "听到这个消息他很伤心。", exPinyin: "Tīngdào zhège xiāoxi tā hěn shāngxīn.", exTrans: "He was very sad to hear this news." },
            { hanzi: "耐心", pinyin: "nàixīn", meaning: "sabar", exHanzi: "老师耐心地解答了问题。", exPinyin: "Lǎoshī nàixīn de jiědá le wèntí.", exTrans: "The teacher answered the question patiently." },
            { hanzi: "信心", pinyin: "xìnxīn", meaning: "percaya diri", exHanzi: "我对这次考试很有信心。", exPinyin: "Wǒ duì zhè cì kǎoshì hěn yǒu xìnxīn.", exTrans: "I have great confidence in this exam." },
            { hanzi: "中心", pinyin: "zhōngxīn", meaning: "pusat", exHanzi: "我们住在市中心。", exPinyin: "Wǒmen zhù zài shì zhōngxīn.", exTrans: "We live in the city center." },
            { hanzi: "粗心", pinyin: "cūxīn", meaning: "ceroboh", exHanzi: "做题时不能太粗心。", exPinyin: "Zuò tí shí bù néng tài cūxīn.", exTrans: "Don't be too careless when solving problems." },
            { hanzi: "马虎", pinyin: "mǎhu", meaning: "ceroboh", exHanzi: "他办事总是马马虎虎的。", exPinyin: "Tā bànshì zǒngshì mǎmǎhūhū de.", exTrans: "He is always careless when doing things." },
            { hanzi: "关心", pinyin: "guānxīn", meaning: "memperhatikan", exHanzi: "谢谢大家对我的关心。", exPinyin: "Xièxie dàjiā duì wǒ de guānxīn.", exTrans: "Thank you all for your care and concern." },
            { hanzi: "地图", pinyin: "dìtú", meaning: "peta", exHanzi: "请用手机打开电子地图。", exPinyin: "Qǐng yòng shǒujī dǎkāi diànzǐ dìtú.", exTrans: "Please open the electronic map on your phone." },
            { hanzi: "电子邮件", pinyin: "diànzǐ yóujiàn", meaning: "email", exHanzi: "我已经给你发了电子邮件。", exPinyin: "Wǒ yǐjīng gěi nǐ fā le diànzǐ yóujiàn.", exTrans: "I have already sent you an email." },
            { hanzi: "动物", pinyin: "dòngwù", meaning: "hewan", exHanzi: "熊猫是我最喜欢的动物。", exPinyin: "Xióngmāo shì wǒ zuì xǐhuan de dòngwù.", exTrans: "Panda is my favorite animal." },
            { hanzi: "段", pinyin: "duàn", meaning: "paragraf", exHanzi: "请阅读下面这段话。", exPinyin: "Qǐng yuèdú xiàmiàn zhè duàn huà.", exTrans: "Please read the paragraph below." },
            { hanzi: "短", pinyin: "duǎn", meaning: "pendek", exHanzi: "冬天的时间感觉很短。", exPinyin: "Dōngtiān de shíjiān gǎnjué hěn duǎn.", exTrans: "Winter time feels very short." },
            { hanzi: "锻炼", pinyin: "duànliàn", meaning: "olahraga", exHanzi: "坚持锻炼身体好。", exPinyin: "Jiānchí duànliàn shēntǐ hǎo.", exTrans: "Persisting in exercising is good for health." },
            { hanzi: "饿", pinyin: "è", meaning: "laper", exHanzi: "我饿了，想吃东西。", exPinyin: "Wǒ è le, xiǎng chī dōngxi.", exTrans: "I am hungry, I want to eat something." },
            { hanzi: "耳朵", pinyin: "ěrduo", meaning: "telinga", exHanzi: "兔子的耳朵很长。", exPinyin: "Tùzi de ěrduo hěn cháng.", exTrans: "Rabbits' ears are very long." },
            { hanzi: "发烧", pinyin: "fāshāo", meaning: "demam", exHanzi: "他感冒发烧了，需要休息。", exPinyin: "Tā gǎnmào fāshāo le, xūyào xiūxi.", exTrans: "He has a cold and fever, he needs rest." },
            { hanzi: "发现", pinyin: "fāxiàn", meaning: "menemukan", exHanzi: "我发现他最近变了。", exPinyin: "Wǒ fāxiàn tā zuìjìn biàn le.", exTrans: "I found that he has changed recently." },
            { hanzi: "方便", pinyin: "fāngbiàn", meaning: "convenient", exHanzi: "坐地铁出行很方便。", exPinyin: "Zuò dìtiě chūxíng hěn fāngbiàn.", exTrans: "Traveling by subway is very convenient." },
            { hanzi: "顺便", pinyin: "shùnbiàn", meaning: "sekalian", exHanzi: "我去买菜，顺便买牛奶。", exPinyin: "Wǒ qù mǎi cài, shùnbiàn mǎi niúnǎi.", exTrans: "I am buying groceries and will get milk along the way." },
            { hanzi: "便宜", pinyin: "piányi", meaning: "cheap", exHanzi: "这件衣服真便宜。", exPinyin: "Zhè jiàn yīfu zhēn piányi.", exTrans: "This clothing is really cheap." },
            { hanzi: "随便", pinyin: "suíbiàn", meaning: "terserah", exHanzi: "你可以随便坐。", exPinyin: "Nǐ kěyǐ suíbiàn zuò.", exTrans: "You can sit wherever you like." },
            { hanzi: "附近", pinyin: "fùjìn", meaning: "dekat", exHanzi: "我家附近有一个公园。", exPinyin: "Wǒ jiā fùjìn yǒu yí gè gōngyuán.", exTrans: "There is a park near my home." },
            { hanzi: "感冒", pinyin: "gǎnmào", meaning: "flu", exHanzi: "天气冷了，小心感冒。", exPinyin: "Tiānqì lěng le, xiǎoxīn gǎnmào.", exTrans: "The weather turned cold, be careful not to catch a cold." },
            { hanzi: "感兴趣", pinyin: "gǎn xīngqù", meaning: "tertarik", exHanzi: "我对中国历史很感兴趣。", exPinyin: "Wǒ duì Zhōngguó lìshǐ hěn gǎn xīngqù.", exTrans: "I am very interested in Chinese history." },
            { hanzi: "根据", pinyin: "gēnjù", meaning: "berdasarkan", exHanzi: "根据规定，这里不能停车。", exPinyin: "Gēnjù guīdìng, zhèlǐ bù néng tíngchē.", exTrans: "According to regulations, parking is not allowed here." },
            { hanzi: "更", pinyin: "gèng", meaning: "lebih", exHanzi: "明天天气会更好。", exPinyin: "Míngtiān tiānqì huì gèng hǎo.", exTrans: "Tomorrow's weather will be even better." },
            { hanzi: "使", pinyin: "shǐ", meaning: "membuat", exHanzi: "这个消息使大家很高兴。", exPinyin: "Zhège xiāoxi shǐ dàjiā hěn kāixīn.", exTrans: "This news made everyone very happy." },
            { hanzi: "便", pinyin: "biàn", meaning: "nyaman", exHanzi: "如果方便，请来找我。", exPinyin: "Rúguǒ fāngbiàn, qǐng lái zhǎo wǒ.", exTrans: "If convenient, please come find me." },
            { hanzi: "故事", pinyin: "gùshi", meaning: "cerita", exHanzi: "奶奶给我讲了一个故事。", exPinyin: "Nǎinai gěi wǒ jiǎng le yí gè gùshi.", exTrans: "Grandma told me a story." },
            { hanzi: "事故", pinyin: "shìgù", meaning: "kecelakaan", exHanzi: "路上发生了一起交通事故。", exPinyin: "Lùshang fāshēng le yì qǐ jiāotōng shìgù.", exTrans: "A traffic accident happened on the road." },
            { hanzi: "关于", pinyin: "guānyú", meaning: "mengenai", exHanzi: "这是一本关于中国文化的书。", exPinyin: "Zhè shì yì běn guānyú Zhōngguó wénhuà de shū.", exTrans: "This is a book about Chinese culture." },
            { hanzi: "航班", pinyin: "hángbān", meaning: "penerbangan", exHanzi: "我的航班准时起飞了。", exPinyin: "Wǒ de hángbān zhǔnshí qǐfēi le.", exTrans: "My flight took off on time." },
            { hanzi: "黑板", pinyin: "hēibǎn", meaning: "papan tulis hitam", exHanzi: "老师在黑板上写字。", exPinyin: "Lǎoshī zài hēibǎn shàng xiězì.", exTrans: "The teacher writes on the blackboard." },
            { hanzi: "甚至", pinyin: "shènzhì", meaning: "bahkan", exHanzi: "他太忙了，甚至没时间吃饭。", exPinyin: "Tā tài máng le, shènzhì méi shíjiān chīfàn.", exTrans: "He is so busy he didn't even have time to eat." },
            { hanzi: "环境", pinyin: "huánjìng", meaning: "lingkungan", exHanzi: "这里的自然环境非常好。", exPinyin: "Zhèlǐ de zìrán huánjìng fēicháng hǎo.", exTrans: "The natural environment here is very good." },
            { hanzi: "换", pinyin: "huàn", meaning: "menukar", exHanzi: "我想换一下零钱。", exPinyin: "Wǒ xiǎng huàn yíxià língqián.", exTrans: "I want to exchange some loose change." },
            { hanzi: "还", pinyin: "huán", meaning: "mengembalikan", exHanzi: "记得把书还给图书馆。", exPinyin: "Jìde bǎ shū huán gěi túshūguǎn.", exTrans: "Remember to return the book to the library." },
            { hanzi: "会议", pinyin: "huìyì", meaning: "rapat", exHanzi: "下午三点有一个重要会议。", exPinyin: "Xiàwǔ sāndiǎn yǒu yí gè zhòngyào huìyì.", exTrans: "There is an important meeting at 3 PM." },
            { hanzi: "回忆", pinyin: "huíyì", meaning: "mengenang", exHanzi: "这里留下了美好的回忆。", exPinyin: "Zhèlǐ liúxià le měihǎo de huíyì.", exTrans: "Good memories were left here." },
            { hanzi: "几乎", pinyin: "jīhū", meaning: "hampir", exHanzi: "我几乎不敢相信这个事实。", exPinyin: "Wǒ jīhū bù gǎn xiāngxìn zhège shìshí.", exTrans: "I could hardly believe this fact." },
            { hanzi: "机会", pinyin: "jīhuì", meaning: "kesempatan", exHanzi: "这是一个难得的机会。", exPinyin: "Zhè shì yí gè nándé de jīhuì.", exTrans: "This is a rare opportunity." },
            { hanzi: "极", pinyin: "jí", meaning: "sangat", exHanzi: "今天的风景美极了。", exPinyin: "Jīntiān de fēngjǐng měi jí le.", exTrans: "Today's scenery is extremely beautiful." },
            { hanzi: "季节", pinyin: "jìjié", meaning: "musim", exHanzi: "春天是我最喜欢的季节。", exPinyin: "Chūntiān shì wǒ zuì xǐhuan de jìjié.", exTrans: "Spring is my favorite season." },
            { hanzi: "检查", pinyin: "jiǎnchá", meaning: "mengecek", exHanzi: "请仔细检查你的试卷。", exPinyin: "Qǐng zǐxì jiǎnchá nǐ de shìjuàn.", exTrans: "Please carefully check your exam paper." },
            { hanzi: "见面", pinyin: "jiànmiàn", meaning: "menemui", exHanzi: "我们很久没有见面了。", exPinyin: "Wǒmen hěn jiǔ méiyǒu jiànmiàn le.", exTrans: "We haven't seen each other for a long time." },
            { hanzi: "降落", pinyin: "jiàngluò", meaning: "turun", exHanzi: "飞机安全降落在机场。", exPinyin: "Fēijī ānquán jiàngluò zài jīchǎng.", exTrans: "The airplane landed safely at the airport." },
            { hanzi: "脚", pinyin: "jiǎo", meaning: "kaki", exHanzi: "我走了很久，脚有点痛。", exPinyin: "Wǒ zǒu le hěn jiǔ, jiǎo yǒudiǎnr tòng.", exTrans: "I walked for a long time and my feet hurt a bit." },
            { hanzi: "接", pinyin: "jiē", meaning: "menerima", exHanzi: "我去机场接一位朋友。", exPinyin: "Wǒ qù jīchǎng jiē yí wèi péngyou.", exTrans: "I am going to the airport to pick up a friend." },
            { hanzi: "街道", pinyin: "jiēdào", meaning: "jalan", exHanzi: "街道两旁种满了树。", exPinyin: "Jiēdào liǎngpáng zhòng mǎn le shù.", exTrans: "Both sides of the street are lined with trees." },
            { hanzi: "结婚", pinyin: "jiéhūn", meaning: "menikah", exHanzi: "他们计划明年结婚。", exPinyin: "Tāmen jìhuà míngnián jiéhūn.", exTrans: "They plan to get married next year." },
            { hanzi: "结束", pinyin: "jiéshù", meaning: "mengakhiri", exHanzi: "会议到此结束。", exPinyin: "Huìyì dào cǐ jiéshù.", exTrans: "The meeting ends here." },
            { hanzi: "解决", pinyin: "jiějué", meaning: "menyelesaikan", exHanzi: "问题终于得到了解决。", exPinyin: "Wèntí zhōngyú dédào le jiějué.", exTrans: "The problem was finally resolved." },
            { hanzi: "借", pinyin: "jiè", meaning: "pinjam", exHanzi: "我可以借用一下你的笔吗？", exPinyin: "Wǒ kěyǐ jièyòng yíxià nǐ de bǐ ma?", exTrans: "May I borrow your pen?" },
            { hanzi: "久", pinyin: "jiǔ", meaning: "tua", exHanzi: "我们认识很久了。", exPinyin: "Wǒmen rènshi hěn jiǔ le.", exTrans: "We have known each other for a long time." },
            { hanzi: "旧", pinyin: "jiù", meaning: "lama", exHanzi: "这件旧衣服该丢了。", exPinyin: "Zhè jiàn jiù yīfu gāi diū le.", exTrans: "This old clothing should be thrown away." },
            { hanzi: "决定", pinyin: "juédìng", meaning: "memutuskan", exHanzi: "我决定留在这里。", exPinyin: "Wǒ juédìng liú zài zhèlǐ.", exTrans: "I decided to stay here." },
            { hanzi: "刻", pinyin: "kè", meaning: "seperempat", exHanzi: "现在是五点一刻。", exPinyin: "Xiànzài shì wǔdiǎn yí kè.", exTrans: "It is a quarter past five now." },
            { hanzi: "客人", pinyin: "kèrén", meaning: "tamu", exHanzi: "家里来客人了。", exPinyin: "Jiālǐ lái kèrén le.", exTrans: "Guests came to our house." },
            { hanzi: "裤子", pinyin: "kùzi", meaning: "celana", exHanzi: "这条裤子太长了。", exPinyin: "Zhè tiáo kùzi tài cháng le.", exTrans: "These pants are too long." },
            { hanzi: "脸", pinyin: "liǎn", meaning: "muka", exHanzi: "洗完脸感觉很舒服。", exPinyin: "Xǐ wán liǎn gǎnjué hěn shūfu.", exTrans: "Feeling very comfortable after washing face." },
            { hanzi: "历史", pinyin: "lìshǐ", meaning: "sejarah", exHanzi: "中国有悠久的历史。", exPinyin: "Zhōngguó yǒu yōujiǔ de lìshǐ.", exTrans: "China has a long history." },
            { hanzi: "邻居", pinyin: "línjū", meaning: "tetangga", exHanzi: "我的邻居非常友好。", exPinyin: "Wǒ de línjū fēicháng yǒuhǎo.", exTrans: "My neighbor is very friendly." },
            { hanzi: "帽子", pinyin: "màozi", meaning: "topi", exHanzi: "戴上帽子保暖。", exPinyin: "Dài shàng màozi bǎonuǎn.", exTrans: "Put on a hat to keep warm." },
            { hanzi: "年级", pinyin: "niánjí", meaning: "kelas", exHanzi: "我是大学三年级的学生。", exPinyin: "Wǒ shì dàxué sān niánjí de xuésheng.", exTrans: "I am a junior university student." },
            { hanzi: "胖", pinyin: "pàng", meaning: "gemuk", exHanzi: "小猫长胖了许多。", exPinyin: "Xiǎomāo zhǎng pàng le xǔduō.", exTrans: "The kitten has gained a lot of weight." },
            { hanzi: "皮鞋", pinyin: "píxié", meaning: "sepatu kulit", exHanzi: "他穿了一双黑色的皮鞋。", exPinyin: "Tā chuān le yì shuāng hēisè de píxié.", exTrans: "He wore a pair of black leather shoes." },
            { hanzi: "普通话", pinyin: "pǔtōnghuà", meaning: "bahasa mandarin", exHanzi: "她的普通话非常标准。", exPinyin: "Tā de pǔtōnghuà fēicháng biāozhǔn.", exTrans: "Her Mandarin is very standard." },
            { hanzi: "其实", pinyin: "qíshí", meaning: "sebenarnya", exHanzi: "其实事情很简单。", exPinyin: "Qíshí shìqing hěn jiǎndān.", exTrans: "Actually, the matter is very simple." },
            { hanzi: "即使", pinyin: "jíshǐ", meaning: "sekalipun", exHanzi: "即使下雨我也要去。", exPinyin: "Jíshǐ xiàyǔ wǒ yě yào qù.", exTrans: "Even if it rains, I will still go." },
            { hanzi: "起飞", pinyin: "qǐfēi", meaning: "take off", exHanzi: "飞机很快就要起飞了。", exPinyin: "Fēijī hěn kuài jiù yào qǐfēi le.", exTrans: "The plane is taking off soon." },
            { hanzi: "裙子", pinyin: "qúnzi", meaning: "rok", exHanzi: "她穿了一条漂亮红裙子。", exPinyin: "Tā chuān le yì tiáo piàoliang hóng qúnzi.", exTrans: "She wore a beautiful red dress." },
            { hanzi: "舒服", pinyin: "shūfu", meaning: "nyaman", exHanzi: "躺在床上真舒服。", exPinyin: "Tǎng zài chuángshàng zhēn shūfu.", exTrans: "Lying in bed is really comfortable." },
            { hanzi: "叔叔", pinyin: "shūshu", meaning: "paman", exHanzi: "叔叔带我去公园玩。", exPinyin: "Shūshu dài wǒ qù gōngyuán wán.", exTrans: "My uncle took me to the park to play." },
            { hanzi: "树", pinyin: "shù", meaning: "pohon", exHanzi: "院子里种了一棵树。", exPinyin: "Yuànzi lǐ zhòng le yì kē shù.", exTrans: "A tree was planted in the yard." },
            { hanzi: "刷牙", pinyin: "shuāyá", meaning: "sikat gigi", exHanzi: "早晚都要记得刷牙。", exPinyin: "Zǎowǎn dōu yào jìde shuāyá.", exTrans: "Remember to brush your teeth morning and night." },
            { hanzi: "司机", pinyin: "sījī", meaning: "supir", exHanzi: "出租车司机师傅很热情。", exPinyin: "Chūzūchē sījī shīfu hěn rèqíng.", exTrans: "The taxi driver is very warm and welcoming." },
            { hanzi: "体育", pinyin: "tǐyù", meaning: "olahraga", exHanzi: "我非常喜欢体育运动。", exPinyin: "Wǒ fēicháng xǐhuan tǐyù yùndòng.", exTrans: "I really like sports." },
            { hanzi: "腿", pinyin: "tuǐ", meaning: "kaki", exHanzi: "我的腿有点酸。", exPinyin: "Wǒ de tuǐ yǒudiǎnr suān.", exTrans: "My legs are a bit sore." },
            { hanzi: "新闻", pinyin: "xīnwén", meaning: "berita", exHanzi: "爷爷正在看七点新闻。", exPinyin: "Yéye zhèngzài kàn qī diǎn xīnwén.", exTrans: "Grandpa is watching the 7 o'clock news." },
            { hanzi: "饮料", pinyin: "yǐnliào", meaning: "minuman", exHanzi: "你想喝什么饮料？", exPinyin: "Nǐ xiǎng hē shénme yǐnliào?", exTrans: "What drink would you like to have?" },
            { hanzi: "遇到", pinyin: "yùdào", meaning: "ketemu", exHanzi: "我在路上遇到了老同学。", exPinyin: "Wǒ zài lùshang yùdào le lǎo tóngxué.", exTrans: "I ran into an old classmate on the road." },
            { hanzi: "愿意", pinyin: "yuànyì", meaning: "mau", exHanzi: "你愿意和我一起去吗？", exPinyin: "Nǐ yuànyì hé wǒ yìqǐ qù ma?", exTrans: "Are you willing to go with me?" },
            { hanzi: "照顾", pinyin: "zhàogù", meaning: "memelihara/perhatian", exHanzi: "请帮忙照顾我的宠物。", exPinyin: "Qǐng bāngmáng zhàogù wǒ de chǒngwù.", exTrans: "Please help take care of my pet." },
            { hanzi: "中间", pinyin: "zhōngjiān", meaning: "tengah", exHanzi: "请站在中间拍照。", exPinyin: "Qǐng zhàn zài zhōngjiān pāizhào.", exTrans: "Please stand in the middle for the photo." },
            { hanzi: "终于", pinyin: "zhōngyú", meaning: "akhirnya", exHanzi: "我们终于到达了目的地。", exPinyin: "Wǒmen zhōngyú dàodá le mùdìdì.", exTrans: "We finally reached our destination." },
            { hanzi: "嘴", pinyin: "zuǐ", meaning: "bibir", exHanzi: "吃完东西擦擦嘴。", exPinyin: "Chī wán dōngxi cā cā zuǐ.", exTrans: "Wipe your mouth after eating." },
            { hanzi: "安排", pinyin: "ānpái", meaning: "mengatur", exHanzi: "公司安排了培训课程。", exPinyin: "Gōngsī ānpái le péixùn kèchéng.", exTrans: "The company arranged a training course." },
            { hanzi: "按照", pinyin: "ànzhào", meaning: "menurut (aturan)", exHanzi: "请按照说明书操作。", exPinyin: "Qǐng ànzhào shuōmíngshū cāozuò.", exTrans: "Please operate according to the instructions." },
            { hanzi: "棒", pinyin: "bàng", meaning: "bagus", exHanzi: "你的表现真的很棒！", exPinyin: "Nǐ de biǎoxiàn zhēn de hěn bàng!", exTrans: "Your performance was really great!" },
            { hanzi: "保证", pinyin: "bǎozhèng", meaning: "menjamin", exHanzi: "我保证按时交作业。", exPinyin: "Wǒ bǎozhèng ànshí jiāo zuòyè.", exTrans: "I guarantee to submit the homework on time." },
            { hanzi: "抱歉", pinyin: "bàoqiàn", meaning: "meminta maaf", exHanzi: "非常抱歉，我迟到了。", exPinyin: "Fēicháng bàoqiàn, wǒ chídào le.", exTrans: "I am deeply sorry, I am late." },
            { hanzi: "倍", pinyin: "bèi", meaning: "kali", exHanzi: "这里的物价比以前翻了一倍。", exPinyin: "Zhèlǐ de wùjià bǐ yǐqián fān le yí bèi.", exTrans: "Prices here doubled compared to before." },
            { hanzi: "遍", pinyin: "biàn", meaning: "kali", exHanzi: "请把课文再读一遍。", exPinyin: "Qǐng bǎ kèwén zài dú yí biàn.", exTrans: "Please read the text one more time." },
            { hanzi: "标准", pinyin: "biāozhǔn", meaning: "standard", exHanzi: "她的汉语发音非常标准。", exPinyin: "Tā de Hànyǔ fāyīn fēicháng biāozhǔn.", exTrans: "Her Chinese pronunciation is very standard." },
            { hanzi: "表格", pinyin: "biǎogé", meaning: "daftar", exHanzi: "请把表格填写完整。", exPinyin: "Qǐng bǎ biǎogé tiánxiě wánzhěng.", exTrans: "Please fill out the form completely." },
            { hanzi: "表示", pinyin: "biǎoshì", meaning: "menunjukan", exHanzi: "他微笑表示同意。", exPinyin: "Tā wēixiào biǎoshì tóngyì.", exTrans: "He smiled to indicate agreement." },
            { hanzi: "表演", pinyin: "biǎoyǎn", meaning: "pertunjukan", exHanzi: "今晚有精彩的武术表演。", exPinyin: "Jīnwǎn yǒu jīngcǎi de wǔshù biǎoyǎn.", exTrans: "There is a wonderful martial arts show tonight." },
            { hanzi: "表扬", pinyin: "biǎoyáng", meaning: "memuji", exHanzi: "老师表扬了他努力学习。", exPinyin: "Lǎoshī biǎoyáng le tā nǔlì xuéxí.", exTrans: "The teacher praised him for studying hard." },
            { hanzi: "并且", pinyin: "bìngqiě", meaning: "lagi pula", exHanzi: "她聪明并且非常勤奋。", exPinyin: "Tā cōngmíng bìngqiě fēicháng qínfèn.", exTrans: "She is smart and also very diligent." },
            { hanzi: "博士", pinyin: "bóshì", meaning: "doktor", exHanzi: "他在大学攻读博士学位。", exPinyin: "Tā zài dàxué gōngdú bóshì xuéwèi.", exTrans: "He is studying for a doctorate degree." },
            { hanzi: "擦", pinyin: "cā", meaning: "menggosok", exHanzi: "请帮我擦一下桌子。", exPinyin: "Qǐng bāng wǒ cā yíxià zhuōzi.", exTrans: "Please help me wipe the table." },
            { hanzi: "猜", pinyin: "cāi", meaning: "menebak", exHanzi: "你能猜出盒子里是什么吗？", exPinyin: "Nǐ néng cāi chū hézi lǐ shì shénme ma?", exTrans: "Can you guess what's in the box?" },
            { hanzi: "材料", pinyin: "cáiliào", meaning: "bahan", exHanzi: "这份总结材料写得很全面。", exPinyin: "Zhè fèn zǒngjié cáiliào xiě de hěn quánmiàn.", exTrans: "This summary material is written comprehensively." },
            { hanzi: "参观", pinyin: "cānguān", meaning: "mengunjungi", exHanzi: "明天我们去参观故宫。", exPinyin: "Míngtiān wǒmen qù cānguān Gùgōng.", exTrans: "Tomorrow we will visit the Forbidden City." },
            { hanzi: "餐厅", pinyin: "cāntīng", meaning: "restoran", exHanzi: "我们在学校餐厅吃午饭。", exPinyin: "Wǒmen zài xuéxiào cāntīng chī wǔfàn.", exTrans: "We eat lunch in the school cafeteria." },
            { hanzi: "长江", pinyin: "Cháng Jiāng", meaning: "sungai yangtze", exHanzi: "长江是中国第一大河。", exPinyin: "Cháng Jiāng shì Zhōngguó dì-yī dà hé.", exTrans: "The Yangtze River is China's longest river." },
            { hanzi: "成为", pinyin: "chéngwéi", meaning: "menjadi", exHanzi: "他梦想成为一名医生。", exPinyin: "Tā mèngxiǎng chéngwéi yì míng yīshēng.", exTrans: "He dreams of becoming a doctor." },
            { hanzi: "城市", pinyin: "chéngshì", meaning: "kota", exHanzi: "上海是一座现代化大城市。", exPinyin: "Shànghǎi shì yí zuò xiàndàihuà dà chéngshì.", exTrans: "Shanghai is a modern large city." },
            { hanzi: "诚实", pinyin: "chéngshí", meaning: "jujur", exHanzi: "诚实是做人的基本原则。", exPinyin: "Chéngshí shì zuòrén de jīběn yuánzé.", exTrans: "Honesty is the basic principle of life." },
            { hanzi: "乘坐", pinyin: "chéngzuò", meaning: "menumpang", exHanzi: "欢迎乘坐本次列车。", exPinyin: "Huānyíng chéngzuò běn cì lièchē.", exTrans: "Welcome aboard this train." },
            { hanzi: "吃惊", pinyin: "chījīng", meaning: "terkejut", exHanzi: "大家对这个决定感到吃惊。", exPinyin: "Dàjiā duì zhège juédìng gǎndào chījīng.", exTrans: "Everyone was surprised by this decision." },
            { hanzi: "重新", pinyin: "chóngxīn", meaning: "sekali lagi", exHanzi: "请把这篇文章重新写一遍。", exPinyin: "Qǐng bǎ zhè piān wénzhāng chóngxīn xiě yí biàn.", exTrans: "Please rewrite this article again." },
            { hanzi: "出差", pinyin: "chūchāi", meaning: "dalam perjalanan bisnis", exHanzi: "爸爸去北京出差了。", exPinyin: "Bàba qù Běijīng chūchāi le.", exTrans: "Dad went to Beijing on a business trip." },
            { hanzi: "厨房", pinyin: "chúfáng", meaning: "dapur", exHanzi: "妈妈正在厨房做晚饭。", exPinyin: "Māma zhèngzài chúfáng zuò wǎnfàn.", exTrans: "Mom is making dinner in the kitchen." },
            { hanzi: "传真", pinyin: "chuánzhēn", meaning: "fax", exHanzi: "请将文件传真给我。", exPinyin: "Qǐng jiāng wénjiàn chuánzhēn gěi wǒ.", exTrans: "Please fax the document to me." },
            { hanzi: "存", pinyin: "cún", meaning: "menabung/menyimpan", exHanzi: "我把钱存进了银行。", exPinyin: "Wǒ bǎ qián cún jìn le yínháng.", exTrans: "I deposited money into the bank." },
            { hanzi: "错误", pinyin: "cuòwù", meaning: "salah", exHanzi: "要勇于承认自己的错误。", exPinyin: "Yào yǒngyú chéngrèn zìjǐ de cuòwù.", exTrans: "One must be brave to admit one's errors." },
            { hanzi: "打扮", pinyin: "dǎban", meaning: "dandan", exHanzi: "她今天打扮得非常漂亮。", exPinyin: "Tā jīntiān dǎban de fēicháng piàoliang.", exTrans: "She dressed up very beautifully today." },
            { hanzi: "打印", pinyin: "dǎyìn", meaning: "mencetak", exHanzi: "请帮我打印这份合同。", exPinyin: "Qǐng bāng wǒ dǎyìn zhè fèn hétong.", exTrans: "Please help me print this contract." },
            { hanzi: "打招呼", pinyin: "dǎ zhāohu", meaning: "menyapa", exHanzi: "见面时要主动打招呼。", exPinyin: "Jiànmiàn shí yào zhǔdòng dǎ zhāohu.", exTrans: "Initiate greetings when meeting someone." },
            { hanzi: "打针", pinyin: "dǎzhēn", meaning: "menyuntik", exHanzi: "护士正在给病人打针。", exPinyin: "Hùshi zhèngzài gěi bìngrén dǎzhēn.", exTrans: "The nurse is giving an injection to the patient." },
            { hanzi: "大概", pinyin: "dàgài", meaning: "hampir", exHanzi: "他大概十分钟后到达。", exPinyin: "Tā dàgài shí fēnzhōng hòu dàodá.", exTrans: "He will probably arrive in ten minutes." },
            { hanzi: "大使馆", pinyin: "dàshǐguǎn", meaning: "kedutaan besar", exHanzi: "我去大使馆办理签证。", exPinyin: "Wǒ qù dàshǐguǎn bànlǐ qiānzhèng.", exTrans: "I am going to the embassy to apply for a visa." },
            { hanzi: "大约", pinyin: "dàyuē", meaning: "kira-kira", exHanzi: "这本书大约有二百页。", exPinyin: "Zhè běn shū dàyuē yǒu èrbǎi yè.", exTrans: "This book has approximately two hundred pages." },
            { hanzi: "大夫", pinyin: "dàifu", meaning: "dokter", exHanzi: "大夫建议他多运动。", exPinyin: "Dàifu jiànyì tā duō yùndòng.", exTrans: "The doctor advised him to exercise more." },
            { hanzi: "戴", pinyin: "dài", meaning: "memakai", exHanzi: "冬天出门要戴帽子。", exPinyin: "Dōngtiān chūmén yào dài màozi.", exTrans: "Wear a hat when going out in winter." },
            { hanzi: "刀", pinyin: "dāo", meaning: "pisau", exHanzi: "用刀切水果要小心。", exPinyin: "Yòng dāo qiē shuǐguǒ yào xiǎoxīn.", exTrans: "Be careful when using a knife to cut fruit." },
            { hanzi: "到处", pinyin: "dàochù", meaning: "di mana-mana", exHanzi: "春天公园里到处都是花。", exPinyin: "Chūntiān gōngyuán lǐ dàochù dōu shì huā.", exTrans: "Spring flowers are everywhere in the park." },
            { hanzi: "导游", pinyin: "dǎoyóu", meaning: "tour guide", exHanzi: "导游热情地讲解景点的历史。", exPinyin: "Dǎoyóu rèqíng de jiǎngjiě jǐngdiǎn de lìshǐ.", exTrans: "The tour guide warmly explained the scenic spot's history." },
            { hanzi: "倒", pinyin: "dào", meaning: "jatuh", exHanzi: "风太大了，树都被吹倒了。", exPinyin: "Fēng tài dà le, shù dōu bèi chuī dào le.", exTrans: "The wind was so strong that trees blew down." },
            { hanzi: "到底", pinyin: "dàodǐ", meaning: "pada akhirnya", exHanzi: "你到底想去哪里？", exPinyin: "Nǐ dàodǐ xiǎng qù nǎlǐ?", exTrans: "Where on earth do you want to go?" },
            { hanzi: "道歉", pinyin: "dàoqiàn", meaning: "meminta maaf", exHanzi: "我诚恳地向你道歉。", exPinyin: "Wǒ chéngkěn de xiàng nǐ dàoqiàn.", exTrans: "I sincerely apologize to you." },
            { hanzi: "得意", pinyin: "déyì", meaning: "bangga", exHanzi: "取得了成绩也不要得意。", exPinyin: "Qǔdé le chéngjì yě bú yào déyì.", exTrans: "Don't get complacent even if achieved success." },
            { hanzi: "登机牌", pinyin: "dēngjīpái", meaning: "boarding pass", exHanzi: "请出示您的登机牌。", exPinyin: "Qǐng chūshì nín de dēngjīpái.", exTrans: "Please show your boarding pass." },
            { hanzi: "低", pinyin: "dī", meaning: "sedikit", exHanzi: "他低着头不说话。", exPinyin: "Tā dī zhe tóu bù shuōhuà.", exTrans: "He lowered his head without speaking." },
            { hanzi: "地点", pinyin: "dìdiǎn", meaning: "lokasi", exHanzi: "请确定会议的地点。", exPinyin: "Qǐng quèdìng huìyì de dìdiǎn.", exTrans: "Please confirm the location of the meeting." },
            { hanzi: "底", pinyin: "dǐ", meaning: "dasar", exHanzi: "清澈的湖水能看到底。", exPinyin: "Qīngchè de húshuǐ néng kàndào dǐ.", exTrans: "The clear lake water lets you see the bottom." },
            { hanzi: "地址", pinyin: "dìzhǐ", meaning: "alamat", exHanzi: "请把你的家庭地址发给我。", exPinyin: "Qǐng bǎ nǐ de jiātíng dìzhǐ fā gěi wǒ.", exTrans: "Please send me your home address." },
            { hanzi: "调查", pinyin: "diàochá", meaning: "investigasi", exHanzi: "警察正在调查这起案件。", exPinyin: "Jǐngchá zhèngzài diàochá zhè qǐ ànjiàn.", exTrans: "Police are investigating this case." },
            { hanzi: "掉", pinyin: "diào", meaning: "jatuh", exHanzi: "我不小心把钥匙掉了。", exPinyin: "Wǒ bù xiǎoxīn bǎ yàoshi diào le.", exTrans: "I accidentally dropped my keys." },
            { hanzi: "堵车", pinyin: "dǔchē", meaning: "macet", exHanzi: "上下班高峰期容易堵车。", exPinyin: "Shàngxiàbān gāofēngqī róngyì dǔchē.", exTrans: "Rush hours are prone to traffic jams." },
            { hanzi: "肚子", pinyin: "dùzi", meaning: "perut", exHanzi: "我肚子饿得咕咕叫。", exPinyin: "Wǒ dùzi è de gūgū jiào.", exTrans: "My stomach is rumbling with hunger." },
            { hanzi: "发生", pinyin: "fāshēng", meaning: "terjadi", exHanzi: "昨晚发生了什么事？", exPinyin: "Zuówǎn fāshēng le shénme shì?", exTrans: "What happened last night?" },
            { hanzi: "发展", pinyin: "fāzhǎn", meaning: "berkembang", exHanzi: "科技的发展改变了生活。", exPinyin: "Kējì de fāzhǎn gǎibiàn le shēnghuó.", exTrans: "Development of technology changed lives." },
            { hanzi: "烦恼", pinyin: "fánnǎo", meaning: "risau", exHanzi: "别为小事增加烦恼。", exPinyin: "Bié wèi xiǎoshì zēngjiā fánnǎo.", exTrans: "Don't add worries over trivial matters." },
            { hanzi: "放松", pinyin: "fàngsōng", meaning: "rileks", exHanzi: "听音乐可以让人放松心情。", exPinyin: "Tīng yīnyuè kěyǐ ràng rén fàngsōng xīnqíng.", exTrans: "Listening to music relaxes one's mood." },
            { hanzi: "费用", pinyin: "fèiyòng", meaning: "biaya", exHanzi: "本次学费包含所有图书费用。", exPinyin: "Běn cì xuéfèi bāohán suǒyǒu túshū fèiyòng.", exTrans: "Tuition includes all book costs." },
            { hanzi: "符合", pinyin: "fúhé", meaning: "sesuai dengan", exHanzi: "你的条件符合我们的要求。", exPinyin: "Nǐ de tiáojiàn fúhé wǒmen de yāoqiú.", exTrans: "Your conditions meet our requirements." },
            { hanzi: "付款", pinyin: "fùkuǎn", meaning: "membayar", exHanzi: "您选择扫码付款吗？", exPinyin: "Nín xuǎnzé sǎomǎ fùkuǎn ma?", exTrans: "Do you choose to pay by scanning code?" },
            { hanzi: "负责", pinyin: "fùzé", meaning: "tanggung jawab", exHanzi: "他是一个非常负责的人。", exPinyin: "Tā shì yí gè fēicháng fùzé de rén.", exTrans: "He is a very responsible person." },
            { hanzi: "复印", pinyin: "fùyìn", meaning: "fotokopi", exHanzi: "请把这页复印三份。", exPinyin: "Qǐng bǎ zhè yè fùyìn sān fèn.", exTrans: "Please photocopy this page 3 times." },
            { hanzi: "赶", pinyin: "gǎn", meaning: "mengejar", exHanzi: "我们要赶快去赶公交车。", exPinyin: "Wǒmen yào gǎnkuài qù gǎn gōngjiāochē.", exTrans: "We must hurry to catch the bus." },
            { hanzi: "敢", pinyin: "gǎn", meaning: "berani", exHanzi: "他不敢独自在夜里出门。", exPinyin: "Tā bù gǎn dúzì zài yèlǐ chūmén.", exTrans: "He doesn't dare go out alone at night." },
            { hanzi: "感动", pinyin: "gǎndòng", meaning: "mengharukan", exHanzi: "这部电影让人非常感动。", exPinyin: "Zhè bù diànyǐng ràng rén fēicháng gǎndòng.", exTrans: "This movie is deeply moving." },
            { hanzi: "感觉", pinyin: "gǎnjué", meaning: "merasa", exHanzi: "今天感觉舒服多了。", exPinyin: "Jīntiān gǎnjué shūfu duō le.", exTrans: "Feeling much better today." },
            { hanzi: "感情", pinyin: "gǎnqíng", meaning: "perasaan", exHanzi: "他们的感情非常好。", exPinyin: "Tāmen de gǎnqíng fēicháng hǎo.", exTrans: "Their emotional bond is very strong." },
            { hanzi: "感谢", pinyin: "gǎnxiè", meaning: "berterimakasih", exHanzi: "非常感谢您的热情帮助。", exPinyin: "Fēicháng gǎnxiè nín de rèqíng bāngzhù.", exTrans: "Thank you very much for your warm help." },
            { hanzi: "高级", pinyin: "gāojí", meaning: "tingkat", exHanzi: "这家高级酒店设备齐全。", exPinyin: "Zhè jiā gāojí jiǔdiàn shèbèi qíquán.", exTrans: "This high-end hotel is well equipped." },
            { hanzi: "高速公路", pinyin: "gāosù gōnglù", meaning: "jalan bebas hambatan", exHanzi: "开车走高速公路更快。", exPinyin: "Kāichē zǒu gāosù gōnglù gèng kuài.", exTrans: "Driving on the highway is faster." },
            { hanzi: "功夫", pinyin: "gōngfu", meaning: "kung fu", exHanzi: "他从小就开始练中国功夫。", exPinyin: "Tā cóngxiǎo jiù kāishǐ liàn Zhōngguó gōngfu.", exTrans: "He practiced Chinese kung fu since childhood." },
            { hanzi: "估计", pinyin: "gūjì", meaning: "memperkiranan", exHanzi: "我估计今天不会下雨。", exPinyin: "Wǒ gūjì jīntiān bú huì xiàyǔ.", exTrans: "I estimate it will not rain today." },
            { hanzi: "预计", pinyin: "yùjì", meaning: "di perkirakan", exHanzi: "预计项目将于下月完成。", exPinyin: "Yùjì xiàngmù jiāng yú xiàyuè wánchéng.", exTrans: "Project expected to finish next month." },
            { hanzi: "鼓励", pinyin: "gǔlì", meaning: "inspirasi/dorongan", exHanzi: "老师鼓励我们多开口说汉语。", exPinyin: "Lǎoshī gǔlì wǒmen duō kāikǒu shuō Hànyǔ.", exTrans: "The teacher encourages us to speak Chinese." },
            { hanzi: "故意", pinyin: "gùyì", meaning: "sengaja", exHanzi: "我不是故意打破杯子的。", exPinyin: "Wǒ bú shì gùyì dǎpò bēizi de.", exTrans: "I didn't break the cup intentionally." },
            { hanzi: "顾客", pinyin: "gùkè", meaning: "pelanggan", exHanzi: "这家店对顾客态度非常好。", exPinyin: "Zhè jiā diàn duì gùkè tàidu fēicháng hǎo.", exTrans: "This store has a great attitude toward customers." },
            { hanzi: "挂", pinyin: "guà", meaning: "menggantungkan", exHanzi: "把衣服挂在衣架上。", exPinyin: "Bǎ yīfu guà zài yījià shàng.", exTrans: "Hang the clothes on the hanger." },
            { hanzi: "关键", pinyin: "guānjiàn", meaning: "kunci/letak persoalan", exHanzi: "态度是成功的关键。", exPinyin: "Tàidu shì chénggōng de guānjiàn.", exTrans: "Attitude is the key to success." },
            { hanzi: "观众", pinyin: "guānzhòng", meaning: "penonton", exHanzi: "台下的观众鼓起了掌。", exPinyin: "Tái xià de guānzhòng gǔ qǐ le zhǎng.", exTrans: "The audience below applauded." },
            { hanzi: "管理", pinyin: "guǎnlǐ", meaning: "mengurus", exHanzi: "管理好时间非常重要。", exPinyin: "Guǎnlǐ hǎo shíjiān fēicháng zhòngyào.", exTrans: "Managing time well is very important." },
            { hanzi: "广播", pinyin: "guǎngbō", meaning: "menyiarkan", exHanzi: "广播里正播放着音乐。", exPinyin: "Guǎngbō lǐ zhèng biāofàng zhe yīnyuè.", exTrans: "Music is currently playing on the radio." },
            { hanzi: "逛", pinyin: "guàng", meaning: "jalan jalan", exHanzi: "周末我和朋友去逛街。", exPinyin: "Zhōumò wǒ hé péngyou qù guàngjiē.", exTrans: "I go shopping with friends on weekends." },
            { hanzi: "规定", pinyin: "guīdìng", meaning: "menetapkan", exHanzi: "大家必须遵守学校规定。", exPinyin: "Dàjiā bìxū zūnshǒu xuéxiào guīdìng.", exTrans: "Everyone must obey school rules." },
            { hanzi: "国籍", pinyin: "guójí", meaning: "kewarganegaraan", exHanzi: "请在表格中填写您的国籍。", exPinyin: "Qǐng zài biǎogé zhōng tiánxiě nín de guójí.", exTrans: "Please fill in your nationality on the form." },
            { hanzi: "国际", pinyin: "guójì", meaning: "international", exHanzi: "北京是一个国际化大都市。", exPinyin: "Běijīng shì yí gè guójìhuà dà dūshì.", exTrans: "Beijing is an international metropolis." },
            { hanzi: "精彩", pinyin: "jīngcǎi", meaning: "luar biasa", exHanzi: "足球比赛非常精彩。", exPinyin: "Zúqiú bǐsài fēicháng jīngcǎi.", exTrans: "The soccer match was extremely exciting." },
            { hanzi: "过程", pinyin: "guòchéng", meaning: "proses", exHanzi: "学习的过程比结果更重要。", exPinyin: "Xuéxí de guòchéng bǐ jiéguǒ gèng zhòngyào.", exTrans: "Learning process matters more than result." },
            { hanzi: "害羞", pinyin: "hàixiū", meaning: "malu", exHanzi: "小姑娘害羞地低下了头。", exPinyin: "Xiǎo gūniang hàixiū de dī xià le tóu.", exTrans: "The little girl shyly lowered her head." },
            { hanzi: "寒假", pinyin: "hánjià", meaning: "liburan musim dingin", exHanzi: "今年寒假你打算做什么？", exPinyin: "Jīnnián hánjià nǐ dǎsuàn zuò shénme?", exTrans: "What do you plan to do this winter break?" },
            { hanzi: "汗", pinyin: "hàn", meaning: "keringat", exHanzi: "跑完步后他出了一身汗。", exPinyin: "Pǎo wán bù hòu tā chū le yì shēn hàn.", exTrans: "He broke into a sweat after running." },
            { hanzi: "合格", pinyin: "hégé", meaning: "memenuhi syarat", exHanzi: "他的产品全部合格。", exPinyin: "Tā de chǎnpǐn quánbù hégé.", exTrans: "His products all passed qualification." },
            { hanzi: "后悔", pinyin: "hòuhuǐ", meaning: "menyesali", exHanzi: "没听你的劝告，我现在很后悔。", exPinyin: "Méi tīng nǐ de quàngào, wǒ xiànzài hěn hòuhuǐ.", exTrans: "I regret not listening to your advice." },
            { hanzi: "厚", pinyin: "hòu", meaning: "tebal", exHanzi: "冬天需要穿厚衣服。", exPinyin: "Dōngtiān xūyào chuān hòu yīfu.", exTrans: "Need to wear thick clothes in winter." },
            { hanzi: "薄的", pinyin: "báode", meaning: "tipis", exHanzi: "这张纸太薄了。", exPinyin: "Zhè zhāng zhǐ tài báo le.", exTrans: "This paper is too thin." },
            { hanzi: "互联网", pinyin: "hùliánwǎng", meaning: "internet", exHanzi: "互联网方便了我们的生活。", exPinyin: "Hùliánwǎng fāngbiàn le wǒmen de shēnghuó.", exTrans: "The internet facilitated our lives." },
            { hanzi: "怀疑", pinyin: "huáiyí", meaning: "meragukan", exHanzi: "我怀疑这个消息不准确。", exPinyin: "Wǒ huáiyí zhège xiāoxi bù zhǔnquè.", exTrans: "I doubt this news is accurate." },
            { hanzi: "活泼", pinyin: "huópō", meaning: "lincah", exHanzi: "这个小女孩性格很活泼。", exPinyin: "Zhège xiǎo nǚhái xìnggé hěn huópō.", exTrans: "This little girl is very lively." },
            { hanzi: "获得", pinyin: "huòdé", meaning: "mendapat", exHanzi: "他在比赛中获得了第一名。", exPinyin: "Tā zài bǐsài zhōng huòdé le dì-yī míng.", exTrans: "He won first place in the competition." },
            { hanzi: "积极", pinyin: "jījí", meaning: "aktif", exHanzi: "要以积极的态度面对困难。", exPinyin: "Yào yǐ jījí de tàidu miànduì kùnnan.", exTrans: "Face difficulties with an active attitude." },
            { hanzi: "积累", pinyin: "jīlěi", meaning: "mengakumulasi", exHanzi: "工作中要注重积累经验。", exPinyin: "Gōngzuò zhōng yào zhùzhòng jīlěi jīngyàn.", exTrans: "Focus on accumulating experience at work." },
            { hanzi: "基础", pinyin: "jīchǔ", meaning: "mendasar", exHanzi: "打好语言基础非常重要。", exPinyin: "Dǎ hǎo yǔyán jīchǔ fēicháng zhòngyào.", exTrans: "Laying a solid language foundation is crucial." },
            { hanzi: "激动", pinyin: "jīdòng", meaning: "terharu", exHanzi: "获奖时他激动得流下了眼泪。", exPinyin: "Huòjiǎng shí tā jīdòng de liú xià le yǎnlèi.", exTrans: "He was so excited that he shed tears." },
            { hanzi: "及时", pinyin: "jíshí", meaning: "segera", exHanzi: "幸亏你及时提醒了我。", exPinyin: "Xìngkuī nǐ jíshí tíxǐng le wǒ.", exTrans: "Fortunately, you reminded me in time." },
            { hanzi: "计算机", pinyin: "jìsuànjī", meaning: "komputer", exHanzi: "他在大学学计算机专业。", exPinyin: "Tā zài dàxué xué jìsuànjī zhuānyè.", exTrans: "He majors in computer science at university." },
            { hanzi: "计算器", pinyin: "jìsuànqì", meaning: "kalkulator", exHanzi: "做数学题可以使用计算器。", exPinyin: "Zuò shùxué tí kěyǐ shǐyòng jìsuànqì.", exTrans: "You can use a calculator for math tasks." },
            { hanzi: "记者", pinyin: "jìzhě", meaning: "reporter", exHanzi: "一位记者正在采访专家。", exPinyin: "Yí wèi jìzhě zhèngzài cǎifǎng zhuānjiā.", exTrans: "A reporter is interviewing an expert." },
            { hanzi: "技术", pinyin: "jìshù", meaning: "teknik", exHanzi: "他的驾驶技术非常高超。", exPinyin: "Tā de jiàshǐ jìshù fēicháng gāochāo.", exTrans: "His driving skills are superb." },
            { hanzi: "既然", pinyin: "jìrán", meaning: "karena sudah", exHanzi: "既然决定了，就坚持到底。", exPinyin: "Jìrán juédìng le, jiù jiānchí dàodǐ.", exTrans: "Since decided, stick to it to the end." },
            { hanzi: "继续", pinyin: "jìxù", meaning: "continue", exHanzi: "休息一会儿后继续工作。", exPinyin: "Xiūxi yíhuìr hòu jìxù gōngzuò.", exTrans: "Continue working after taking a short rest." },
            { hanzi: "家具", pinyin: "jiājù", meaning: "perabotan", exHanzi: "新买的家具已经到了。", exPinyin: "Xīn mǎi de jiājù yǐjīng dào le.", exTrans: "The newly bought furniture has arrived." },
            { hanzi: "坚持", pinyin: "jiānchí", meaning: "memengang teguh", exHanzi: "坚持就是胜利。", exPinyin: "Jiānchí jiùshì shènglì.", exTrans: "Perseverance means victory." },
            { hanzi: "将来", pinyin: "jiānglái", meaning: "masa depan", exHanzi: "你将来想从事什么职业？", exPinyin: "Nǐ jiānglái xiǎng cóngshì shénme zhíyè?", exTrans: "What career do you want in the future?" },
            { hanzi: "奖金", pinyin: "jiǎngjīn", meaning: "hadiah", exHanzi: "年底发了不少奖金。", exPinyin: "Niándǐ fā le bù shǎo jiǎngjīn.", exTrans: "A lot of bonuses were distributed at year end." },
            { hanzi: "降低", pinyin: "jiàngdī", meaning: "menurunkan", exHanzi: "我们要尽量降低成本。", exPinyin: "Wǒmen yào jìnliàng jiàngdī chéngběn.", exTrans: "We should try best to reduce costs." },
            { hanzi: "交流", pinyin: "jiāoliú", meaning: "berkomunikasi", exHanzi: "多和朋友交流思想。", exPinyin: "Duō hé péngyou jiāoliú sīxiǎng.", exTrans: "Exchange thoughts with friends often." },
            { hanzi: "郊区", pinyin: "jiāoqū", meaning: "daerah pinggir", exHanzi: "郊区的空气比市区新鲜。", exPinyin: "Jiāoqū de kōngqì bǐ shìqū xīnxiān.", exTrans: "The air in suburbs is fresher than downtown." },
            { hanzi: "骄傲", pinyin: "jiāoào", meaning: "sombong", exHanzi: "取得了成绩也不能骄傲。", exPinyin: "Qǔdé le chéngjì yě bù néng jiāo'ào.", exTrans: "Don't be arrogant even with achievements." },
            { hanzi: "教授", pinyin: "jiàoshòu", meaning: "profesor", exHanzi: "张教授在台上做演讲。", exPinyin: "Zhāng jiàoshòu zài táishàng zuò yǎnjiǎng.", exTrans: "Professor Zhang gives a speech on stage." },
            { hanzi: "接受", pinyin: "jiēshòu", meaning: "menerima", exHanzi: "我接受你的诚恳建议。", exPinyin: "Wǒ jiēshòu nǐ de chéngkěn jiànyì.", exTrans: "I accept your sincere suggestion." },
            { hanzi: "接着", pinyin: "jiēzhe", meaning: "selanjutnya", exHanzi: "他说完后，接着往下做。", exPinyin: "Tā shuō wán hòu, jiēzhe wǎng xià zuò.", exTrans: "After he finished speaking, he proceeded." },
            { hanzi: "节约", pinyin: "jiéyuē", meaning: "menghemat", exHanzi: "我们要节约用水。", exPinyin: "Wǒmen yào jiéyuē yòngshuǐ.", exTrans: "We must conserve water." },
            { hanzi: "结果", pinyin: "jiéguǒ", meaning: "hasil", exHanzi: "比赛的结果让人满意。", exPinyin: "Bǐsài de jiéguǒ ràng rén mǎnyì.", exTrans: "The match result was satisfying." },
            { hanzi: "解释", pinyin: "jiěshì", meaning: "menjelaskan", exHanzi: "请向大家解释一下原因。", exPinyin: "Qǐng xiàng dàjiā jiěshì yíxià yuányīn.", exTrans: "Please explain the reason to everyone." },
            { hanzi: "尽管", pinyin: "jǐnguǎn", meaning: "walaupun", exHanzi: "尽管天黑了，他还在工作。", exPinyin: "Jǐnguǎn tiān hēi le, tā hái zài gōngzuò.", exTrans: "Although dark, he is still working." },
            { hanzi: "紧张", pinyin: "jǐnzhāng", meaning: "tegang", exHanzi: "第一次上台我很紧张。", exPinyin: "Dì-yī cì shàngtái wǒ hěn jǐnzhāng.", exTrans: "I was nervous on stage the first time." },
            { hanzi: "进行", pinyin: "jìnxíng", meaning: "melaksanakan", exHanzi: "实验正在顺利进行。", exPinyin: "Shíyàn zhèngzài shùnlì jìnxíng.", exTrans: "The experiment is proceeding smoothly." },
            { hanzi: "京剧", pinyin: "jīngjù", meaning: "orang peking", exHanzi: "京剧是中国的传统戏剧。", exPinyin: "Jīngjù shì Zhōngguó de chuántǒng xìjù.", exTrans: "Peking Opera is China's traditional opera." },
            { hanzi: "经济", pinyin: "jīngjì", meaning: "ekonomi", exHanzi: "近几年国家经济快速发展。", exPinyin: "Jìn jǐ nián guójiā jīngjì kuàisù fāzhǎn.", exTrans: "The economy developed fast recently." },
            { hanzi: "经历", pinyin: "jīnglì", meaning: "pengalaman", exHanzi: "这次旅行是一次难忘的经历。", exPinyin: "Zhè cì lǚxíng shì yí cì nánwàng de jīnglì.", exTrans: "This trip was an unforgettable experience." },
            { hanzi: "经验", pinyin: "jīngyàn", meaning: "pengalaman", exHanzi: "他在教学方面很有经验。", exPinyin: "Tā zài jiàoxué fāngmiàn hěn yǒu jīngyàn.", exTrans: "He has much experience in teaching." },
            { hanzi: "景色", pinyin: "jǐngsè", meaning: "pemandangan", exHanzi: "山顶的景色非常壮观。", exPinyin: "Shāndǐng de jǐngsè fēicháng zhuàngguān.", exTrans: "The scenery from the top is magnificent." },
            { hanzi: "风景", pinyin: "fēngjǐng", meaning: "pemandangan", exHanzi: "沿途的风景十分美丽。", exPinyin: "Yántú de fēngjǐng shífēn měilì.", exTrans: "The scenery along the route is beautiful." },
            { hanzi: "竞争", pinyin: "jìngzhēng", meaning: "bersaing", exHanzi: "市场竞争越来越激烈。", exPinyin: "Shìchǎng jìngzhēng yuè lái yuè jīliè.", exTrans: "Market competition is growing intense." },
            { hanzi: "鉴定", pinyin: "jiàndìng", meaning: "authentication", exHanzi: "专家对这幅字画进行了鉴定。", exPinyin: "Zhuānjiā duì zhè fú zìhuà jìnxíng le jiàndìng.", exTrans: "Experts authenticated this artwork." },
            { hanzi: "居然", pinyin: "jūrán", meaning: "secara tak terduga", exHanzi: "没想到他居然成功了！", exPinyin: "Méi xiǎngdào tā jūrán chénggōng le!", exTrans: "Unexpectedly, he actually succeeded!" },
            { hanzi: "镜子", pinyin: "jìngzi", meaning: "cermin", exHanzi: "照镜子整理一下头发。", exPinyin: "Zhào jìngzi zhěnglǐ yíxià tóufa.", exTrans: "Look in the mirror to tidy your hair." },
            { hanzi: "究竟", pinyin: "jiūjìng", meaning: "sesungguhnya", exHanzi: "你究竟有什么打算？", exPinyin: "Nǐ jiūjìng yǒu shénme dǎsuàn?", exTrans: "What exactly are your plans?" },
            { hanzi: "举", pinyin: "jǔ", meaning: "mengangkat", exHanzi: "请大家举手发言。", exPinyin: "Qǐng dàjiā jǔshǒu fāyán.", exTrans: "Please raise hands to speak." },
            { hanzi: "举办", pinyin: "jǔbàn", meaning: "mengadakan", exHanzi: "学校下周举办运动会。", exPinyin: "Xuéxiào xiàzhōu jǔbàn yùndònghuì.", exTrans: "School will hold sports games next week." },
            { hanzi: "拒绝", pinyin: "jùjué", meaning: "menolak", exHanzi: "我礼貌地拒绝了他的邀请。", exPinyin: "Wǒ lǐmào de jùjué le tā de yāoqǐng.", exTrans: "I politely declined his invitation." },
            { hanzi: "距离", pinyin: "jùlí", meaning: "berjarak", exHanzi: "这里距离机场大约三十公里。", exPinyin: "Zhèlǐ jùlí jīchǎng dàyuē sānshí gōnglǐ.", exTrans: "It is about 30 km from airport." },
            { hanzi: "聚会", pinyin: "jùhuì", meaning: "pertemuan", exHanzi: "今晚有一个同学聚会。", exPinyin: "Jīnwǎn yǒu yí gè tóngxué jùhuì.", exTrans: "There is a classmate reunion tonight." },
            { hanzi: "科学", pinyin: "kēxué", meaning: "ilmu pengetahuan", exHanzi: "我们要相信科学。", exPinyin: "Wǒmen yào xiāngxìn kēxué.", exTrans: "We must believe in science." },
            { hanzi: "棵", pinyin: "kē", meaning: "satuan tanaman", exHanzi: "路边种着一棵大树。", exPinyin: "Lùbiān zhòng zhe yì kē dà shù.", exTrans: "A large tree grows by the roadside." },
            { hanzi: "可怜", pinyin: "kělián", meaning: "kasihan", exHanzi: "这只流浪小猫看起来真可怜。", exPinyin: "Zhè zhī liúlàng xiǎomāo kàn qǐlái zhēn kělián.", exTrans: "This stray kitten looks pitiful." },
            { hanzi: "可惜", pinyin: "kěxī", meaning: "eman", exHanzi: "错过了这场演出真可惜。", exPinyin: "Cuòguò le zhè chǎng yǎnchū zhēn kěxī.", exTrans: "Pity to miss this show." },
            { hanzi: "肯定", pinyin: "kěndìng", meaning: "pasti", exHanzi: "只要努力就肯定能成功。", exPinyin: "Zhǐyào nǔlì jiù kěndìng néng chénggōng.", exTrans: "With effort, success is definite." },
            { hanzi: "恐怕", pinyin: "kǒngpà", meaning: "mungkin", exHanzi: "今天恐怕要下雨，带伞吧。", exPinyin: "Jīntiān kǒngpà yào xiàyǔ, dài sǎn ba.", exTrans: "I fear it will rain today, take umbrella." },
            { hanzi: "矿泉水", pinyin: "kuàngquánshuǐ", meaning: "air mineral", exHanzi: "请给我一瓶矿泉水。", exPinyin: "Qǐng gěi wǒ yì píng kuàngquánshuǐ.", exTrans: "Please give me a bottle of mineral water." },
            { hanzi: "来不及", pinyin: "láibují", meaning: "tak sempat", exHanzi: "快走，不然来不及赶火车了。", exPinyin: "Kuài zǒu, bùrán láibují gǎn huǒchē le.", exTrans: "Hurry up or we won't make the train." },
            { hanzi: "来得及", pinyin: "láidejí", meaning: "sempat", exHanzi: "还有半小时，完全来得及。", exPinyin: "Hái yǒu bàn xiǎoshí, wánquán láidejí.", exTrans: "30 minutes left, plenty of time." },
            { hanzi: "懒", pinyin: "lǎn", meaning: "males", exHanzi: "不要太懒，多出去运动。", exPinyin: "Bú yào tài lǎn, duō chūqù yùndòng.", exTrans: "Don't be lazy, go out to exercise." },
            { hanzi: "冷静", pinyin: "lěngjìng", meaning: "tenang", exHanzi: "遇到急事要保持冷静。", exPinyin: "Yùdào jíshì yào bǎochí lěngjìng.", exTrans: "Keep calm when encountering emergencies." },
            { hanzi: "离婚", pinyin: "líhūn", meaning: "cerai", exHanzi: "他们由于性格不合离婚了。", exPinyin: "Tāmen yóuyú xìnggé bùhé líhūn le.", exTrans: "They divorced due to incompatible personalities." },
            { hanzi: "理发", pinyin: "lǐfǎ", meaning: "potong rambut", exHanzi: "他的头发长了，要去理发。", exPinyin: "Tā de tóufa cháng le, yào qù lǐfǎ.", exTrans: "His hair grew long, needs a haircut." },
            { hanzi: "理想", pinyin: "lǐxiǎng", meaning: "ideal", exHanzi: "通过努力实现自己的理想。", exPinyin: "Tōngguò nǔlì shíxiàn zìjǐ de lǐxiǎng.", exTrans: "Realize ideals through hard work." },
            { hanzi: "联系", pinyin: "liánxì", meaning: "berkomunikasi", exHanzi: "有事请随时跟我联系。", exPinyin: "Yǒu shì qǐng suíshí gēn wǒ liánxì.", exTrans: "Feel free to contact me if needed." },
            { hanzi: "两", pinyin: "liǎng", meaning: "sejuk", exHanzi: "我有两个好朋友。", exPinyin: "Wǒ yǒu liǎng gè hǎo péngyou.", exTrans: "I have two good friends." },
            { hanzi: "流利", pinyin: "liúlì", meaning: "lancar", exHanzi: "能说一口流利的汉语。", exPinyin: "Néng shuō yì kǒu liúlì de Hànyǔ.", exTrans: "Can speak fluent Chinese." },
            { hanzi: "流", pinyin: "liú", meaning: "mengalir", exHanzi: "河水向东流去。", exPinyin: "Héshuǐ xiàng dōng liú qù.", exTrans: "The river flows to the east." },
            { hanzi: "流行", pinyin: "liúxíng", meaning: "tren/populer", exHanzi: "这首歌曲最近非常流行。", exPinyin: "Zhè shǒu gēqǔ zuìjìn fēicháng liúxíng.", exTrans: "This song is very popular recently." },
            { hanzi: "乱", pinyin: "luàn", meaning: "kacau", exHanzi: "房间太乱了，赶紧收拾一下。", exPinyin: "Fángjiān tài luàn le, gǎnjǐn shōushi yíxià.", exTrans: "The room is messy, clean it up." },
            { hanzi: "麻烦", pinyin: "máfan", meaning: "repot", exHanzi: "真不好意思，给你添麻烦了。", exPinyin: "Zhēn bù hǎoyìsi, gěi nǐ tiān máfan le.", exTrans: "Sorry for causing you trouble." },
            { hanzi: "满", pinyin: "mǎn", meaning: "penuh", exHanzi: "水杯里倒满了热茶。", exPinyin: "Shuǐbēi lǐ dào mǎn le rè chá.", exTrans: "The cup was filled with hot tea." },
            { hanzi: "毛巾", pinyin: "máojīn", meaning: "handuk", exHanzi: "用毛巾擦干脸上的水。", exPinyin: "Yòng máojīn cā gān liǎn shàng de shuǐ.", exTrans: "Wipe water off face with a towel." },
            { hanzi: "美丽", pinyin: "měilì", meaning: "indah", exHanzi: "公园里的风景非常美丽。", exPinyin: "Gōngyuán lǐ de fēngjǐng fēicháng měilì.", exTrans: "Scenery in the park is beautiful." },
            { hanzi: "梦", pinyin: "mèng", meaning: "meng-mimpi", exHanzi: "我昨晚做了一个奇妙的梦。", exPinyin: "Wǒ zuówǎn zuò le yí gè qímiào de mèng.", exTrans: "I had a wonderful dream last night." },
            { hanzi: "迷路", pinyin: "mílù", meaning: "tersesat", exHanzi: "我在大雾中迷路了。", exPinyin: "Wǒ zài dàwù zhōng mílù le.", exTrans: "I got lost in the heavy fog." },
            { hanzi: "密码", pinyin: "mìmǎ", meaning: "password", exHanzi: "请不要把银行卡密码告诉别人。", exPinyin: "Qǐng bù yào bǎ yínhángkǎ mìmǎ gàosu biérén.", exTrans: "Don't share bank PIN with others." },
            { hanzi: "民族", pinyin: "mínzú", meaning: "bangsa", exHanzi: "中国是一个多民族国家。", exPinyin: "Zhōngguó shì yí gè duō mínzú guójiā.", exTrans: "China is a multi-ethnic nation." },
            { hanzi: "目的", pinyin: "mùdì", meaning: "tujuan", exHanzi: "我们学习的目的是掌握知识。", exPinyin: "Wǒmen xuéxí de mùdì shì zhǎngwò zhīshi.", exTrans: "Our learning purpose is mastering knowledge." },
            { hanzi: "拿", pinyin: "ná", meaning: "mengambil", exHanzi: "请帮我把那本书拿过来。", exPinyin: "Qǐng bāng wǒ bǎ nà běn shū ná guòlái.", exTrans: "Please bring that book to me." },
            { hanzi: "难", pinyin: "nán", meaning: "susah", exHanzi: "这道数学题对我来说太难了。", exPinyin: "Zhè dào shùxué tí duì wǒ lái shuō tài nán le.", exTrans: "This math problem is too hard for me." },
            { hanzi: "难道", pinyin: "nándào", meaning: "apakah", exHanzi: "难道你真的不知道这件事？", exPinyin: "Nándào nǐ zhēn de bù zhīdào zhè jiàn shì?", exTrans: "Do you really not know about this?" },
            { hanzi: "鸟", pinyin: "niǎo", meaning: "burung", exHanzi: "小鸟在树枝上欢快地唱歌。", exPinyin: "Xiǎoniǎo zài shùzhī shàng huānkuài de chànggē.", exTrans: "Birds sing cheerfully on branches." },
            { hanzi: "努力", pinyin: "nǔlì", meaning: "berusaha", exHanzi: "只有努力学习才能取得好成绩。", exPinyin: "Zhǐyǒu nǔlì xuéxí cái néng qǔdé hǎo chéngjì.", exTrans: "Only hard study gets good grades." },
            { hanzi: "爬山", pinyin: "páshān", meaning: "mendaki gunung", exHanzi: "周末我们打算去爬山。", exPinyin: "Zhōumò wǒmen dǎsuàn qù páshān.", exTrans: "We plan to climb mountains on weekend." },
            { hanzi: "盘子", pinyin: "pánzi", meaning: "piring", exHanzi: "请把水果装在盘子里。", exPinyin: "Qǐng bǎ shuǐguǒ zhuāng zài pánzi lǐ.", exTrans: "Please put fruit on the plate." },
            { hanzi: "啤酒", pinyin: "píjiǔ", meaning: "bir", exHanzi: "夏天喝冰啤酒很解暑。", exPinyin: "Xiàtiān hē bīng píjiǔ hěn jiěshǔ.", exTrans: "Drinking ice beer cools summer heat." },
            { hanzi: "其他", pinyin: "qítā", meaning: "lainnya", exHanzi: "除了他，其他人都到了。", exPinyin: "Chúle tā, qítā rén dōu dào le.", exTrans: "Except him, all others arrived." },
            { hanzi: "其中", pinyin: "qízhōng", meaning: "di antaranya", exHanzi: "我买了几本书，其中有一本是历史书。", exPinyin: "Wǒ mǎi le jǐ běn shū, qízhōng yǒu yì běn shì lìshǐ shū.", exTrans: "I bought books; one is history." },
            { hanzi: "情况", pinyin: "qíngkuàng", meaning: "keadaan", exHanzi: "请跟我说明一下现场的情况。", exPinyin: "Qǐng gēn wǒ shuōmíng yíxià xiànchǎng de qíngkuàng.", exTrans: "Please explain the on-site condition." },
            { hanzi: "请假", pinyin: "qǐngjià", meaning: "izin", exHanzi: "他身体不舒服，向公司请假了。", exPinyin: "Tā shēntǐ bù shūfu, xiàng gōngsī qǐngjià le.", exTrans: "He requested sick leave from company." },
            { hanzi: "请客", pinyin: "qǐngkè", meaning: "traktir", exHanzi: "今天发工资，我请客！", exPinyin: "Jīntiān fā gōngzī, wǒ qǐngkè!", exTrans: "Paid today, my treat!" },
            { hanzi: "穷", pinyin: "qióng", meaning: "miskin", exHanzi: "虽然穷，但他过得很快乐。", exPinyin: "Suīrán qióng, dàn tā guò de hěn kuàilè.", exTrans: "Though poor, he lives happily." },
            { hanzi: "区别", pinyin: "qūbié", meaning: "perbedaan", exHanzi: "你能看出这两张图的区别吗？", exPinyin: "Nǐ néng kàn chū zhè liǎng zhāng tú de qūbié ma?", exTrans: "Can you spot difference between two pictures?" },
            { hanzi: "取", pinyin: "qǔ", meaning: "mengambil", exHanzi: "我去快递站取包裹。", exPinyin: "Wǒ qù kuàidìzhàn qǔ bāoguǒ.", exTrans: "I go to pickup parcel at station." },
            { hanzi: "全", pinyin: "quán", meaning: "seluruh", exHanzi: "全家人聚在一起吃晚饭。", exPinyin: "Quán jiārén jù zài yìqǐ chī wǎnfàn.", exTrans: "Whole family gathered for dinner." },
            { hanzi: "然后", pinyin: "ránhòu", meaning: "kemudian", exHanzi: "先洗手，然后再吃东西。", exPinyin: "Xiān xǐshǒu, ránhòu zài chī dōngxi.", exTrans: "Wash hands first, then eat." },
            { hanzi: "热情", pinyin: "rèqíng", meaning: "ramah/antusias", exHanzi: "主人热情地招待了我们。", exPinyin: "Zhǔrén rèqíng de zhāodài le wǒmen.", exTrans: "The host warmly entertained us." },
            { hanzi: "认为", pinyin: "rènwéi", meaning: "berpendapat", exHanzi: "我认为这个方案可行。", exPinyin: "Wǒ rènwéi zhège fāng'àn kěxíng.", exTrans: "I consider this plan feasible." },
            { hanzi: "认真", pinyin: "rènzhēn", meaning: "serius", exHanzi: "对待学习一定要态度认真。", exPinyin: "Duìdài xuéxí yídìng yào tàidu rènzhēn.", exTrans: "Be earnest toward learning." },
            { hanzi: "容易", pinyin: "róngyì", meaning: "gampang", exHanzi: "这道题很容易做。", exPinyin: "Zhè dào tí hěn róngyì zuò.", exTrans: "This problem is easy to do." },
            { hanzi: "如果", pinyin: "rúguǒ", meaning: "jika", exHanzi: "如果明天不下雨，我们就去郊游。", exPinyin: "Rúguǒ míngtiān bù xiàyǔ, wǒmen jiù qù jiāoyóu.", exTrans: "If no rain tomorrow, we go outing." },
            { hanzi: "伞", pinyin: "sǎn", meaning: "payung", exHanzi: "下雨了，出门记得带伞。", exPinyin: "Xiàyǔ le, chūmén jìde dài sǎn.", exTrans: "It rains, remember to bring umbrella." },
            { hanzi: "上网", pinyin: "shàngwǎng", meaning: "internet", exHanzi: "我喜欢上网查资料。", exPinyin: "Wǒ xǐhuan shàngwǎng chá zīliào.", exTrans: "I like surfing net for data." },
            { hanzi: "稍微", pinyin: "shāowēi", meaning: "sedikit", exHanzi: "请稍微等我一下。", exPinyin: "Qǐng shāowēi děng wǒ yíxià.", exTrans: "Please wait for me a short while." },
            { hanzi: "社会", pinyin: "shèhuì", meaning: "masyarakat", exHanzi: "我们要学会适应社会发展。", exPinyin: "Wǒmen yào xuéhuì shìyìng shèhuì fāzhǎn.", exTrans: "Learn to adapt to social development." },
            { hanzi: "深", pinyin: "shēn", meaning: "dalam", exHanzi: "这条河很深，游泳要小心。", exPinyin: "Zhè tiáo hé hěn shēn, yóuyǒng yào xiǎoxīn.", exTrans: "River is deep, swim carefully." },
            { hanzi: "申请", pinyin: "shēnqǐng", meaning: "mengajukan", exHanzi: "我申请了去国外留学的机会。", exPinyin: "Wǒ shēnqǐng le qù guówài liúxué de jīhuì.", exTrans: "Applied for studying abroad opportunity." },
            { hanzi: "生活", pinyin: "shēnghuó", meaning: "kehidupan", exHanzi: "在这里生活非常便利。", exPinyin: "Zài zhèlǐ shēnghuó fēicháng biànlì.", exTrans: "Living here is very convenient." },
            { hanzi: "生意", pinyin: "shēngyi", meaning: "bisnis", exHanzi: "祝你的生意越来越兴隆。", exPinyin: "Zhù nǐ de shēngyi yuè lái yuè xīnglóng.", exTrans: "Wish your business prospers." },
            { hanzi: "省", pinyin: "shěng", meaning: "provinsi", exHanzi: "江苏省位于中国东部。", exPinyin: "Jiāngsū Shěng wèiyú Zhōngguó dōngbù.", exTrans: "Jiangsu Province is in east China." },
            { hanzi: "剩", pinyin: "shèng", meaning: "sisa", exHanzi: "桌上还剩下一块蛋糕。", exPinyin: "Zhuōshàng hái shèngxià yí kuài dàngāo.", exTrans: "One piece of cake left on table." },
            { hanzi: "失败", pinyin: "shībài", meaning: "gagal", exHanzi: "失败是成功之母。", exPinyin: "Shībài shì chénggōng zhī mǔ.", exTrans: "Failure is the mother of success." },
            { hanzi: "师傅", pinyin: "shīfu", meaning: "guru/tukang", exHanzi: "请问师傅，去火车站怎么走？", exPinyin: "Qǐngwèn shīfu, qù huǒchēzhàn zěnme zǒu?", exTrans: "Master driver, how to train station?" },
            { hanzi: "十分", pinyin: "shífēn", meaning: "sangat", exHanzi: "他对这个结果感到十分满意。", exPinyin: "Tā duì zhège jiéguǒ gǎndào shífēn mǎnyì.", exTrans: "He feels extremely satisfied with result." },
            { hanzi: "实际", pinyin: "shíjì", meaning: "aktual", exHanzi: "结合实际情况制定计划。", exPinyin: "Jiéhé shíjì qíngkuàng zhìdìng jìhuà.", exTrans: "Formulate plans considering actual situations." },
            { hanzi: "时候", pinyin: "shíhòu", meaning: "waktu", exHanzi: "你什么时候有空？", exPinyin: "Nǐ shénme shíhòu yǒu kòng?", exTrans: "When are you free?" },
            { hanzi: "时间", pinyin: "shíjiān", meaning: "waktu", exHanzi: "时间过得真快！", exPinyin: "Shíjiān guò de zhēn kuài!", exTrans: "Time passes so fast!" },
            { hanzi: "实在", pinyin: "shízài", meaning: "sebenarnya", exHanzi: "我实在想不出更好的办法了。", exPinyin: "Wǒ shízài xiǎng bù chū gèng hǎo de bànfǎ le.", exTrans: "I really can't think of better way." },
            { hanzi: "使用", pinyin: "shǐyòng", meaning: "menggunakan", exHanzi: "请按照说明使用这台机器。", exPinyin: "Qǐng ànzhào shuōmíng shǐyòng zhè tái jīqì.", exTrans: "Use machine according to instructions." },
            { hanzi: "世纪", pinyin: "shìjì", meaning: "abad", exHanzi: "二十一世纪是信息时代。", exPinyin: "Èrshíyī shìjì shì xìnxī shídài.", exTrans: "21st century is information age." },
            { hanzi: "适应", pinyin: "shìyìng", meaning: "beradaptasi", exHanzi: "他很快适应了新环境。", exPinyin: "Tā hěn kuài shìyìng le xīn huánjìng.", exTrans: "He adapted to new environment quickly." },
            { hanzi: "事情", pinyin: "shìqing", meaning: "urusan", exHanzi: "今天有很多事情要做。", exPinyin: "Jīntiān yǒu hěn duō shìqing yào zuò.", exTrans: "Many things to do today." },
            { hanzi: "收", pinyin: "shōu", meaning: "menerima", exHanzi: "我已经收到了你的来信。", exPinyin: "Wǒ yǐjīng shōudào le nǐ de láixìn.", exTrans: "I have received your letter." },
            { hanzi: "收到", pinyin: "shōudào", meaning: "menerima", exHanzi: "收到请回复。", exPinyin: "Shōudào qǐng huífù.", exTrans: "Please reply upon receipt." },
            { hanzi: "收入", pinyin: "shōurù", meaning: "pendapatan", exHanzi: "他的月收入增加了不少。", exPinyin: "Tā de yuè shōurù zēngjiā le bù shǎo.", exTrans: "His monthly income increased significantly." },
            { hanzi: "手", pinyin: "shǒu", meaning: "tangan", exHanzi: "饭前要洗手。", exPinyin: "Fàn qián yào xǐshǒu.", exTrans: "Wash hands before meals." },
            { hanzi: "手机", pinyin: "shǒujī", meaning: "hp", exHanzi: "我的手机没电了。", exPinyin: "Wǒ de shǒujī méi diàn le.", exTrans: "My phone battery is dead." },
            { hanzi: "受到", pinyin: "shòudào", meaning: "mendapatkan", exHanzi: "他的演讲收到了大家的热烈欢迎。", exPinyin: "Tā de yǎnjiǎng shōudào le dàjiā de rèliè huānyíng.", exTrans: "His speech received warm welcome." },
            { hanzi: "数学", pinyin: "shùxué", meaning: "matematika", exHanzi: "他的数学成绩非常好。", exPinyin: "Tā de shùxué chéngjì fēicháng hǎo.", exTrans: "His math score is excellent." },
            { hanzi: "双", pinyin: "shuāng", meaning: "sepasang", exHanzi: "我买了一双新鞋。", exPinyin: "Wǒ mǎi le yì shuāng xīn xié.", exTrans: "I bought a pair of new shoes." },
            { hanzi: "水平", pinyin: "shuǐpíng", meaning: "level/kadar", exHanzi: "他的汉语水平提高很快。", exPinyin: "Tā de Hànyǔ shuǐpíng tígāo hěn kuài.", exTrans: "His Chinese level improved quickly." },
            { hanzi: "太阳", pinyin: "tàiyáng", meaning: "matahari", exHanzi: "早晨的太阳冉冉升起。", exPinyin: "Zǎochen de tàiyáng rǎnrǎn shēngqǐ.", exTrans: "Morning sun rises slowly." },
            { hanzi: "态度", pinyin: "tàidù", meaning: "sikap", exHanzi: "工作态度决定成败。", exPinyin: "Gōngzuò tàidù juédìng chéngbài.", exTrans: "Work attitude determines success/failure." },
            { hanzi: "谈", pinyin: "tán", meaning: "berbicara", exHanzi: "他们正在书房谈事情。", exPinyin: "Tāmen zhèngzài shūfáng tán shìqing.", exTrans: "They are talking about matters in study." },
            { hanzi: "弹钢琴", pinyin: "tán gāngqín", meaning: "main piano", exHanzi: "妹妹从小就学习弹钢琴。", exPinyin: "Mèimei cóngxiǎo jiù xuéxí tán gāngqín.", exTrans: "Sister learned piano since young." },
            { hanzi: "汤", pinyin: "tāng", meaning: "sup", exHanzi: "这碗鸡汤非常鲜美。", exPinyin: "Zhè wǎn jītāng fēicháng xiānměi.", exTrans: "This chicken soup is delicious." },
            { hanzi: "条件", pinyin: "tiáojiàn", meaning: "syarat", exHanzi: "这里的住宿条件不错。", exPinyin: "Zhèlǐ de zhùsù tiáojiàn búcuò.", exTrans: "Accommodation condition here is good." },
            { hanzi: "提高", pinyin: "tígāo", meaning: "meningkatkan", exHanzi: "多听广播可以提高听力水平。", exPinyin: "Duō tīng guǎngbō kěyǐ tígāo tīnglì shuǐpíng.", exTrans: "Listening radio improves listening skill." },
            { hanzi: "提供", pinyin: "tígōng", meaning: "menyediakan", exHanzi: "酒店免费提供早餐。", exPinyin: "Jiǔdiàn miǎnfèi tígōng zǎocān.", exTrans: "Hotel provides free breakfast." },
            { hanzi: "提前", pinyin: "tíqián", meaning: "lebih dulu", exHanzi: "请提前十分钟到达考场。", exPinyin: "Qǐng tíqián shí fēnzhōng dàodá kǎochǎng.", exTrans: "Arrive 10 mins early at exam room." },
            { hanzi: "提醒", pinyin: "tíxǐng", meaning: "mengingatkan", exHanzi: "谢谢你提醒我带钥匙。", exPinyin: "Xièxie nǐ tíxǐng wǒ dài yàoshi.", exTrans: "Thanks for reminding me keys." },
            { hanzi: "填空", pinyin: "tiánkòng", meaning: "mengisi titik2", exHanzi: "请回答下面的填空题。", exPinyin: "Qǐng huídá xiàmiàn de tiánkòng tí.", exTrans: "Answer fill-in-the-blank question." },
            { hanzi: "条", pinyin: "tiáo", meaning: "helai/batang", exHanzi: "河里有一条小鱼。", exPinyin: "Hélǐ yǒu yì tiáo xiǎoyú.", exTrans: "There is a small fish in the river." },
            { hanzi: "同事", pinyin: "tóngshì", meaning: "rekan kerja", exHanzi: "我和同事们关系相处融洽。", exPinyin: "Wǒ hé tóngshìmen guānxi xiāngchǔ róngqià.", exTrans: "Get along well with colleagues." },
            { hanzi: "同意", pinyin: "tóngyì", meaning: "setuju", exHanzi: "经理同意了我的请假申请。", exPinyin: "Jīnglǐ tóngyì le wǒ de qǐngjià shēnqǐng.", exTrans: "Manager agreed leave request." },
            { hanzi: "突然", pinyin: "tūrán", meaning: "tiba-tiba", exHanzi: "天空突然下起了大雨。", exPinyin: "Tiānkōng tūrán xià qǐ le dàyǔ.", exTrans: "Sky suddenly started heavy rain." },
            { hanzi: "图书馆", pinyin: "túshūguǎn", meaning: "perpustakaan", exHanzi: "我喜欢去图书馆看书。", exPinyin: "Wǒ xǐhuan qù túshūguǎn kànshū.", exTrans: "I like reading at library." },
            { hanzi: "推", pinyin: "tuī", meaning: "dorong", exHanzi: "请推开门进去。", exPinyin: "Qǐng tuī kāi mén jìnqù.", exTrans: "Push the door open and go in." },
            { hanzi: "完成", pinyin: "wánchéng", meaning: "menyelesaikan", exHanzi: "我们按时完成了任务。", exPinyin: "Wǒmen ànshí wánchéng le rènwu.", exTrans: "We completed task on time." },
            { hanzi: "碗", pinyin: "wǎn", meaning: "mangkuk", exHanzi: "服务员，请给我拿一个空碗。", exPinyin: "Fúwùyuán, qǐng gěi wǒ ná yí gè kōng wǎn.", exTrans: "Waiter, please bring empty bowl." },
            { hanzi: "万", pinyin: "wàn", meaning: "puluh ribu", exHanzi: "这座城市有一百万人口。", exPinyin: "Zhè zuò chéngshì yǒu yìbǎi wàn rénkǒu.", exTrans: "City has 1 million population." },
            { hanzi: "忘记", pinyin: "wàngjì", meaning: "lupa", exHanzi: "别忘记关门。", exPinyin: "Bié wàngjì guān mén.", exTrans: "Don't forget to close door." },
            { hanzi: "为", pinyin: "wèi", meaning: "demi/untuk", exHanzi: "我们要为人民服务。", exPinyin: "Wǒmen yào wèi rénmín fúwù.", exTrans: "We should serve the people." },
            { hanzi: "为了", pinyin: "wèile", meaning: "demi", exHanzi: "为了健康，要坚持锻炼。", exPinyin: "Wèile jiànkāng, yào jiānchí duànliàn.", exTrans: "Exercise for good health." },
            { hanzi: "位", pinyin: "wèi", meaning: "orang", exHanzi: "这位是我们的新老师。", exPinyin: "Zhè wèi shì wǒmen de xīn lǎoshī.", exTrans: "This is our new teacher." },
            { hanzi: "文化", pinyin: "wénhuà", meaning: "budaya", exHanzi: "体验不同的民间文化。", exPinyin: "Tǐyàn bùtóng de mínjiān wénhuà.", exTrans: "Experience different folk cultures." },
            { hanzi: "问", pinyin: "wèn", meaning: "tanya", exHanzi: "不懂就要及时问老师。", exPinyin: "Bù dǒng jiù yào jíshí wèn lǎoshī.", exTrans: "Ask teacher promptly if not understanding." },
            { hanzi: "问题", pinyin: "wèntí", meaning: "pertanyaan", exHanzi: "你有什么问题吗？", exPinyin: "Nǐ yǒu shénme wèntí ma?", exTrans: "Do you have any questions?" },
            { hanzi: "握手", pinyin: "wòshǒu", meaning: "jabat tangan", exHanzi: "双方代表亲切握手。", exPinyin: "Shuāngfāng dàibiǎo qīnqiè wòshǒu.", exTrans: "Both representatives shook hands cordially." },
            { hanzi: "西红柿", pinyin: "xīhóngshì", meaning: "tomat", exHanzi: "西红柿炒鸡蛋很好吃。", exPinyin: "Xīhóngshì chǎo jīdàn hěn hǎochī.", exTrans: "Tomato scrambled eggs is tasty." },
            { hanzi: "习惯", pinyin: "xíguàn", meaning: "kebiasaan", exHanzi: "养成早起的好习惯。", exPinyin: "Yǎngchéng zǎoqǐ de hǎo xíguàn.", exTrans: "Develop good habit of early rising." },
            { hanzi: "洗手间", pinyin: "xǐshǒujiān", meaning: "toilet", exHanzi: "请问洗手间在哪里？", exPinyin: "Qǐngwèn xǐshǒujiān zài nǎlǐ?", exTrans: "Where is the washroom?" },
            { hanzi: "洗澡", pinyin: "xǐzǎo", meaning: "mandi", exHanzi: "运动后洗澡很舒服。", exPinyin: "Yùndòng hòu xǐzǎo hěn shūfu.", exTrans: "Taking bath after exercise feels good." },
            { hanzi: "现代", pinyin: "xiàndài", meaning: "modern", exHanzi: "现代社会节奏很快。", exPinyin: "Xiàndài shèhuì jiézòu hěn kuài.", exTrans: "Modern society pace is fast." },
            { hanzi: "香蕉", pinyin: "xiāngjiāo", meaning: "pisang", exHanzi: "猴子喜欢吃香蕉。", exPinyin: "Hóuzi xǐhuan chī xiāngjiāo.", exTrans: "Monkeys like eating bananas." },
            { hanzi: "相同", pinyin: "xiāngtóng", meaning: "sama", exHanzi: "我们有着相同的爱好。", exPinyin: "Wǒmen yǒu zhe xiāngtóng de àihào.", exTrans: "We share identical hobbies." },
            { hanzi: "相信", pinyin: "xiāngxìn", meaning: "percaya", exHanzi: "我相信你一定能做到。", exPinyin: "Wǒ xiāngxìn nǐ yídìng néng zuòdào.", exTrans: "I trust you can do it." },
            { hanzi: "像", pinyin: "xiàng", meaning: "seperti", exHanzi: "这孩子长得真像他爸爸。", exPinyin: "Zhè háizi zhǎng de zhēn xiàng tā bàba.", exTrans: "Kid looks just like father." },
            { hanzi: "校长", pinyin: "xiàozhǎng", meaning: "kepala sekolah", exHanzi: "校长在集会上讲话。", exPinyin: "Xiàozhǎng zài jíhuì shàng jiǎnghuà.", exTrans: "Principal speaks at assembly." },
            { hanzi: "鞋", pinyin: "xié", meaning: "sepatu", exHanzi: "穿上舒适的鞋去跑步。", exPinyin: "Chuān shàng shūshì de xié qù pǎobù.", exTrans: "Put comfortable shoes to run." },
            { hanzi: "信", pinyin: "xìn", meaning: "surat/percaya", exHanzi: "我给远方的朋友写了一封信。", exPinyin: "Wǒ gěi yuǎnfāng de péngyou xiě le yì fēng xìn.", exTrans: "Wrote letter to distant friend." },
            { hanzi: "信用卡", pinyin: "xìnyòngkǎ", meaning: "kartu kredit", exHanzi: "这里支持信用卡刷卡付款。", exPinyin: "Zhèlǐ zhīchí xìnyòngkǎ shuākǎ fùkuǎn.", exTrans: "Credit card payment supported here." },
            { hanzi: "行李箱", pinyin: "xínglǐxiāng", meaning: "koper", exHanzi: "把衣服装进行李箱里。", exPinyin: "Bǎ yīfu zhuāng jìn xínglǐxiāng lǐ.", exTrans: "Pack clothes into luggage box." },
            { hanzi: "熊猫", pinyin: "xióngmāo", meaning: "panda", exHanzi: "大熊猫非常可爱。", exPinyin: "Dà xióngmāo fēicháng kě'ài.", exTrans: "Giant pandas are very cute." },
            { hanzi: "需要", pinyin: "xūyào", meaning: "butuh", exHanzi: "你需要什么帮助吗？", exPinyin: "Nǐ xūyào shénme bāngzhù ma?", exTrans: "Do you need any help?" },
            { hanzi: "选择", pinyin: "xuǎnzé", meaning: "pilih", exHanzi: "面临重大的选择。", exPinyin: "Miànlín zhòngdà de xuǎnzé.", exTrans: "Facing a major choice." },
            { hanzi: "要求", pinyin: "yāoqiú", meaning: "permintaan", exHanzi: "严格要求自己。", exPinyin: "Yángé yāoqiú zìjǐ.", exTrans: "Set strict requirements on oneself." },
            { hanzi: "爷爷", pinyin: "yéye", meaning: "kakek", exHanzi: "爷爷在散步。", exPinyin: "Yéye zài sànbù.", exTrans: "Grandpa is taking a walk." },
            { hanzi: "一定", pinyin: "yīdìng", meaning: "pasti", exHanzi: "明天我一定准时来。", exPinyin: "Míngtiān wǒ yídìng zhǔnshí lái.", exTrans: "I will certainly come on time tomorrow." },
            { hanzi: "一共", pinyin: "yīgòng", meaning: "total", exHanzi: "这些商品一共一百元。", exPinyin: "Zhèxiē shāngpǐn yígòng yìbǎi yuán.", exTrans: "Items cost 100 yuan total." },
            { hanzi: "一会儿", pinyin: "yíhuìr", meaning: "sebentar", exHanzi: "请稍等一会儿。", exPinyin: "Qǐng shāo děng yíhuìr.", exTrans: "Please wait a short moment." },
            { hanzi: "一路平安", pinyin: "yílù píng'ān", meaning: "selamat jalan", exHanzi: "祝你一路平安！", exPinyin: "Zhù nǐ yílù píng'ān!", exTrans: "Wish you a safe journey!" },
            { hanzi: "一样", pinyin: "yīyàng", meaning: "sama", exHanzi: "我们俩的选择是一样的。", exPinyin: "Wǒmen liǎ de xuǎnzé shì yíyàng de.", exTrans: "Our two choices are identical." },
            { hanzi: "意见", pinyin: "yìjiàn", meaning: "pendapat", exHanzi: "大家有什么不同的意见？", exPinyin: "Dàjiā yǒu shénme bùtóng de yìjiàn?", exTrans: "Any different opinions from anyone?" },
            { hanzi: "意思", pinyin: "yìsi", meaning: "arti", exHanzi: "这个词是什么意思？", exPinyin: "Zhège cí shì shénme yìsi?", exTrans: "What does this word mean?" },
            { hanzi: "因", pinyin: "yīn", meaning: "karena", exHanzi: "因天气原因航班取消了。", exPinyin: "Yīn tiānqì yuányīn hángbān qūxiāo le.", exTrans: "Flight canceled due to weather." },
            { hanzi: "音乐", pinyin: "yīnyuè", meaning: "musik", exHanzi: "我喜欢听古典音乐。", exPinyin: "Wǒ xǐhuan tīng gǔdiǎn yīnyuè.", exTrans: "I like classical music." },
            { hanzi: "银行", pinyin: "yínháng", meaning: "bank", exHanzi: "我去银行办业务。", exPinyin: "Wǒ qù yínháng bàn yèwù.", exTrans: "I go to bank for business." },
            { hanzi: "应该", pinyin: "yīnggāi", meaning: "seharusnya", exHanzi: "你应该按时吃药。", exPinyin: "Nǐ yīnggāi ànshí chīyào.", exTrans: "You should take medicine on time." },
            { hanzi: "影响", pinyin: "yǐngxiǎng", meaning: "pengaruh", exHanzi: "环境对人的成长有很大影响。", exPinyin: "Huánjìng duì rén de chéngzhǎng yǒu hěn dà yǐngxiǎng.", exTrans: "Environment greatly affects growth." },
            { hanzi: "用", pinyin: "yòng", meaning: "pakai", exHanzi: "请用汉语回答。", exPinyin: "Qǐng yòng Hànyǔ huídá.", exTrans: "Please answer in Chinese." },
            { hanzi: "游戏", pinyin: "yóuxì", meaning: "game", exHanzi: "孩子们在做游戏。", exPinyin: "Háizimen zài zuò yóuxì.", exTrans: "Children play games." },
            { hanzi: "有名", pinyin: "yǒumíng", meaning: "terkenal", exHanzi: "这里是一个非常有名的景点。", exPinyin: "Zhèlǐ shì yí gè fēicháng yǒumíng de jǐngdiǎn.", exTrans: "This is a very famous attraction." },
            { hanzi: "又", pinyin: "yòu", meaning: "lagi", exHanzi: "今天又下雨了。", exPinyin: "Jīntiān yòu xiàyǔ le.", exTrans: "It rained again today." },
            { hanzi: "元", pinyin: "yuán", meaning: "yuan", exHanzi: "这本杂志十五元。", exPinyin: "Zhè běn zázhì shíwǔ yuán.", exTrans: "This magazine costs 15 yuan." },
            { hanzi: "月亮", pinyin: "yuèliàng", meaning: "bulan", exHanzi: "今晚的月亮特别圆。", exPinyin: "Jīnwǎn de yuèliàng tèbié yuán.", exTrans: "The moon tonight is round." },
            { hanzi: "越", pinyin: "yuè", meaning: "semakin", exHanzi: "风越刮越大。", exPinyin: "Fēng yuè guā yuè dà.", exTrans: "Wind blows harder and harder." },
            { hanzi: "云", pinyin: "yún", meaning: "awan", exHanzi: "蓝天飘着朵朵白云。", exPinyin: "Lántiān piāo zhe duǒduǒ bái yún.", exTrans: "White clouds float in blue sky." },
            { hanzi: "站", pinyin: "zhàn", meaning: "berdiri", exHanzi: "请大家站起来。", exPinyin: "Qǐng dàjiā zhàn qǐlái.", exTrans: "Please stand up everyone." },
            { hanzi: "长", pinyin: "zhǎng", meaning: "panjang", exHanzi: "小树长高了。", exPinyin: "Xiǎoshù zhǎng gāo le.", exTrans: "The little tree grew tall." },
            { hanzi: "照片", pinyin: "zhàopiàn", meaning: "foto", exHanzi: "这是一张珍贵的老照片。", exPinyin: "Zhè shì yì zhāng zhēnguì de lǎo zhàopiàn.", exTrans: "This is a precious old photo." },
            { hanzi: "照相机", pinyin: "zhàoxiàngjī", meaning: "kamera", exHanzi: "带上照相机去摄影。", exPinyin: "Dài shàng zhàoxiàngjī qù shèyǐng.", exTrans: "Take camera to take pictures." },
            { hanzi: "者", pinyin: "zhě", meaning: "orang", exHanzi: "志愿者们在帮助老人。", exPinyin: "Zhìyuànzhěmen zài bāngzhù lǎorén.", exTrans: "Volunteers are helping seniors." },
            { hanzi: "真正", pinyin: "zhēnzhèng", meaning: "sebenar", exHanzi: "什么才是真正的朋友？", exPinyin: "Shénme cái shì zhēnzhèng de péngyou?", exTrans: "What constitutes a true friend?" },
            { hanzi: "正常", pinyin: "zhèngcháng", meaning: "normal", exHanzi: "一切都在正常进行。", exPinyin: "Yíqiè dōu zài zhèngcháng jìnxíng.", exTrans: "Everything proceeds normally." },
            { hanzi: "正好", pinyin: "zhènghǎo", meaning: "pas", exHanzi: "你来的正好，我们开饭了。", exPinyin: "Nǐ lái de zhènghǎo, wǒmen kāifàn le.", exTrans: "You arrived right on time for dinner." },
            { hanzi: "正确", pinyin: "zhèngquè", meaning: "benar", exHanzi: "请给出正确的答案。", exPinyin: "Qǐng gěichū zhèngquè de dá'àn.", exTrans: "Please provide the correct answer." },
            { hanzi: "正式", pinyin: "zhèngshì", meaning: "resmi", exHanzi: "会议将于明天正式开始。", exPinyin: "Huìyì jiāng yú míngtiān zhèngshì kāishǐ.", exTrans: "Meeting will officially start tomorrow." },
            { hanzi: "证明", pinyin: "zhèngmíng", meaning: "membuktikan", exHanzi: "事实证明他是正确的。", exPinyin: "Shìshí zhèngmíng tā shì zhèngquè de.", exTrans: "Facts prove he is correct." },
            { hanzi: "芝麻", pinyin: "zhīma", meaning: "wijen", exHanzi: "芝麻烧饼味道很香。", exPinyin: "Zhīma shāobǐng wèi dào hěn xiāng.", exTrans: "Sesame flatbread tastes delicious." },
            { hanzi: "只", pinyin: "zhǐ", meaning: "hanya", exHanzi: "我只有一个要求。", exPinyin: "Wǒ zhǐ yǒu yí gè yāoqiú.", exTrans: "I only have one request." },
            { hanzi: "只好", pinyin: "zhǐhǎo", meaning: "terpaksa", exHanzi: "没有公交车，我只好走路。", exPinyin: "Méiyǒu gōngjiāochē, wǒ zhǐhǎo zǒulù.", exTrans: "No bus, I had to walk." },
            { hanzi: "只有", pinyin: "zhǐyǒu", meaning: "hanya", exHanzi: "只有努力才能成功。", exPinyin: "Zhǐyǒu nǔlì cái néng chénggōng.", exTrans: "Only effort brings success." },
            { hanzi: "种", pinyin: "zhǒng", meaning: "jenis", exHanzi: "这种水果很甜。", exPinyin: "Zhè zhǒng shuǐguǒ hěn tián.", exTrans: "This type of fruit is sweet." },
            { hanzi: "重点", pinyin: "zhòngdiǎn", meaning: "poin utama", exHanzi: "这是今天复习的重点。", exPinyin: "Zhè shì jīntiān fùxí de zhòngdiǎn.", exTrans: "This is review priority today." },
            { hanzi: "重要", pinyin: "zhòngyào", meaning: "penting", exHanzi: "健康是非常重要的。", exPinyin: "Jiànkāng shì fēicháng zhòngyào de.", exTrans: "Health is extremely important." },
            { hanzi: "周末", pinyin: "zhōumò", meaning: "akhir pekan", exHanzi: "祝你周末愉快！", exPinyin: "Zhù nǐ zhōumò yúkuài!", exTrans: "Wish you a happy weekend!" },
            { hanzi: "主要", pinyin: "zhǔyào", meaning: "utama", exHanzi: "主要的原因在于沟通不够。", exPinyin: "Zhǔyào de yuányīn zàiyú gōutōng bú gòu.", exTrans: "Main reason is lack of communication." },
            { hanzi: "注意", pinyin: "zhùyì", meaning: "perhatikan", exHanzi: "请注意听讲。", exPinyin: "Qǐng zhùyì tīngjiǎng.", exTrans: "Please pay attention to the lecture." },
            { hanzi: "祝", pinyin: "zhù", meaning: "mendoakan", exHanzi: "祝你生日快乐！", exPinyin: "Zhù nǐ shēngrì kuàilè!", exTrans: "Wish you happy birthday!" },
            { hanzi: "祝贺", pinyin: "zhùhè", meaning: "selamat", exHanzi: "祝贺你取得了优异成绩！", exPinyin: "Zhùhè nǐ qǔdé le yōuyì chéngjì!", exTrans: "Congrats on excellent grades!" },
            { hanzi: "著名", pinyin: "zhùmíng", meaning: "terkenal", exHanzi: "他是一位著名的科学家。", exPinyin: "Tā shì yí wèi zhùmíng de kēxuéjiā.", exTrans: "He is a famous scientist." },
            { hanzi: "专门", pinyin: "zhuānmén", meaning: "khusus", exHanzi: "这本书是专门写给儿童的。", exPinyin: "Zhè běn shū shì zhuānmén xiě gěi értóng de.", exTrans: "This book is written specifically for kids." },
            { hanzi: "专业", pinyin: "zhuānyè", meaning: "jurusan/profesional", exHanzi: "他在大学学计算机专业。", exPinyin: "Tā zài dàxué xué jìsuànjī zhuānyè.", exTrans: "He majors in CS in college." },
            { hanzi: "转", pinyin: "zhuǎn", meaning: "belok/pindah", exHanzi: "前方路口请向右转。", exPinyin: "Qiánfāng lùkǒu qǐng xiàng yòu zhuǎn.", exTrans: "Turn right at next intersection." },
            { hanzi: "赚", pinyin: "zhuàn", meaning: "mencari uang", exHanzi: "通过打工赚钱。", exPinyin: "Tōngguò dǎgōng zhuànqián.", exTrans: "Earn money through part-time work." },
            { hanzi: "准备", pinyin: "zhǔnbèi", meaning: "siap", exHanzi: "我已经做好了准备。", exPinyin: "Wǒ yǐjīng zuò hǎo le zhǔnbèi.", exTrans: "I am fully prepared." },
            { hanzi: "准确", pinyin: "zhǔnquè", meaning: "akurat", exHanzi: "请准确计算出结果。", exPinyin: "Qǐng zhǔnquè jìsuàn chū jiéguǒ.", exTrans: "Please calculate result accurately." },
            { hanzi: "桌子", pinyin: "zhuōzi", meaning: "meja", exHanzi: "桌子上放着一台电脑。", exPinyin: "Zhuōzi shàng fàng zhe yì tái diànnǎo.", exTrans: "A computer is placed on the table." },
            { hanzi: "准时", pinyin: "zhǔnshí", meaning: "tepat waktu", exHanzi: "大家一定要准时集合。", exPinyin: "Dàjiā yídìng yào zhǔnshí jíhé.", exTrans: "Gather on time strictly." },
            { hanzi: "字", pinyin: "zì", meaning: "huruf", exHanzi: "他的汉字写得非常漂亮。", exPinyin: "Tā de Hànzì xiě de fēicháng piàoliang.", exTrans: "His Chinese characters look beautiful." },
            { hanzi: "字典", pinyin: "zìdiǎn", meaning: "kamus", exHanzi: "查字典了解生字的意思。", exPinyin: "Chá zìdiǎn liǎojiě shēngzì de yìsi.", exTrans: "Consult dictionary for character meanings." },
            { hanzi: "自己", pinyin: "zìjǐ", meaning: "sendiri", exHanzi: "要学会照顾自己。", exPinyin: "Yào xuéhuì zhàogù zìjǐ.", exTrans: "Learn to take care of yourself." },
            { hanzi: "自行车", pinyin: "zìxíngchē", meaning: "sepeda", exHanzi: "我每天骑自行车去上学。", exPinyin: "Wǒ měitiān qí zìxíngchē qù shàngxué.", exTrans: "I ride bicycle to school every day." },
            { hanzi: "总是", pinyin: "zǒngshì", meaning: "selalu", exHanzi: "他总是乐于帮助别人。", exPinyin: "Tā zǒngshì lèyú bāngzhù biérén.", exTrans: "He is always willing to help others." },
            { hanzi: "最后", pinyin: "zuìhòu", meaning: "terakhir", exHanzi: "最后，祝大家一切顺利！", exPinyin: "Zuìhòu, zhù dàjiā yíqiè shùnlì!", exTrans: "Finally, wish everyone smooth success!" },
            { hanzi: "最近", pinyin: "zuìjìn", meaning: "baru-baru ini", exHanzi: "你最近在忙些什么？", exPinyin: "Nǐ zuìjìn zài máng xiē shénme?", exTrans: "What are you busy with recently?" },
            { hanzi: "尊重", pinyin: "zūnzhòng", meaning: "menghormati", exHanzi: "我们要尊重别人的选择。", exPinyin: "Wǒmen yào zūnzhòng biérén de xuǎnzé.", exTrans: "We must respect choices of others." },
            { hanzi: "左边", pinyin: "zuǒbiān", meaning: "kiri", exHanzi: "左边那栋大楼是图书馆。", exPinyin: "Zuǒbiān nà dòng dàlóu shì túshūguǎn.", exTrans: "Building on left is library." },
            { hanzi: "座", pinyin: "zuò", meaning: "seat/gedung", exHanzi: "一座漂亮的大桥。", exPinyin: "Yí zuò piàoliang de dàqiáo.", exTrans: "A beautiful grand bridge." },
            { hanzi: "座位", pinyin: "zuòwèi", meaning: "tempat duduk", exHanzi: "请回自己的座位坐好。", exPinyin: "Qǐng huí zìjǐ de zuòwèi zuò hǎo.", exTrans: "Return to your seat and sit down." }
        ];

        let currentIndex = 0;
        let wrongWords = JSON.parse(localStorage.getItem('hsk4_wrong_words_full')) || [];

        const cardEl = document.getElementById('card');
        const hanziEl = document.getElementById('card-hanzi');
        const pinyinEl = document.getElementById('card-pinyin');
        const meaningEl = document.getElementById('card-meaning');
        
        const exHanziEl = document.getElementById('card-ex-hanzi');
        const exPinyinEl = document.getElementById('card-ex-pinyin');
        const exTransEl = document.getElementById('card-ex-trans');

        const counterEl = document.getElementById('counter');
        const progressEl = document.getElementById('progress');
        const wrongListEl = document.getElementById('wrongList');
        const wrongCountEl = document.getElementById('wrong-count');

        function updateCard() {
            const currentItem = vocabData[currentIndex];
            hanziEl.textContent = currentItem.hanzi;
            pinyinEl.textContent = currentItem.pinyin;
            meaningEl.textContent = currentItem.meaning;

            exHanziEl.textContent = currentItem.exHanzi;
            exPinyinEl.textContent = currentItem.exPinyin;
            exTransEl.textContent = currentItem.exTrans;

            counterEl.textContent = `词语 ${currentIndex + 1} / ${vocabData.length}`;
            progressEl.style.width = `${((currentIndex + 1) / vocabData.length) * 100}%`;

            // 恢复卡片为正面
            cardEl.classList.remove('flipped');
        }

        function flipCard() {
            cardEl.classList.toggle('flipped');
        }

        function nextCard() {
            if (currentIndex < vocabData.length - 1) {
                currentIndex++;
                updateCard();
            } else {
                alert('🎉 恭喜你已经完成了全部 469 个 HSK 4 级词汇的复习！');
                currentIndex = 0;
                updateCard();
            }
        }

        function prevCard() {
            if (currentIndex > 0) {
                currentIndex--;
                updateCard();
            }
        }

        function markCorrect() {
            nextCard();
        }

        function markWrong() {
            const currentItem = vocabData[currentIndex];
            const exists = wrongWords.some(item => item.hanzi === currentItem.hanzi);
            if (!exists) {
                wrongWords.push(currentItem);
                saveAndRenderWrongList();
            }
            nextCard();
        }

        function removeWrong(index, event) {
            event.stopPropagation();
            wrongWords.splice(index, 1);
            saveAndRenderWrongList();
        }

        function saveAndRenderWrongList() {
            localStorage.setItem('hsk4_wrong_words_full', JSON.stringify(wrongWords));
            wrongCountEl.textContent = `${wrongWords.length} 个词`;
            
            if (wrongWords.length === 0) {
                wrongListEl.innerHTML = `<div class="empty-tip">暂无错词，继续加油！💪</div>`;
                return;
            }

            wrongListEl.innerHTML = '';
            wrongWords.forEach((item, index) => {
                const li = document.createElement('li');
                li.className = 'wrong-item';
                li.innerHTML = `
                    <span onclick="jumpToWord('${item.hanzi}')"><strong>${item.hanzi}</strong> (${item.pinyin}) - ${item.meaning}</span>
                    <button class="remove-wrong" onclick="removeWrong(${index}, event)">移出</button>
                `;
                wrongListEl.appendChild(li);
            });
        }

        function jumpToWord(hanzi) {
            const index = vocabData.findIndex(item => item.hanzi === hanzi);
            if (index !== -1) {
                currentIndex = index;
                updateCard();
            }
        }

        // 朗读词语
        function playWordAudio() {
            const currentItem = vocabData[currentIndex];
            speakText(currentItem.hanzi);
        }

        // 朗读例句
        function playExampleAudio() {
            const currentItem = vocabData[currentIndex];
            speakText(currentItem.exHanzi);
        }

        function speakText(text) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                const utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = 'zh-CN';
                utterance.rate = 0.85; // 稍微放慢，便于学习听清
                window.speechSynthesis.speak(utterance);
            } else {
                alert('您的浏览器不支持语音朗读功能');
            }
        }

        // 初始化显示
        updateCard();
        saveAndRenderWrongList();
    </script>
</body>
</html>