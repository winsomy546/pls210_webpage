# pls210_webpage
Interactive research deck webpage for PLS210
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PLS210 Interactive Research Deck — Winsomy546</title>
    <style>
        :root {
            --bg-gradient: radial-gradient(circle at 50% 50%, #1e1b4b 0%, #0b0f19 100%);
            --card-bg: rgba(23, 32, 54, 0.75);
            --accent-cyan: #00f2fe;
            --accent-pink: #ff007f;
            --accent-purple: #7f00ff;
            --accent-yellow: #ffe600;
            --text-main: #f1f5f9;
            --text-muted: #94a3b8;
            --border-glow: rgba(0, 242, 254, 0.4);
        }

        .cyber-theme {
            --bg-gradient: radial-gradient(circle at 50% 50%, #2a0845 0%, #0f051d 100%);
            --card-bg: rgba(40, 15, 60, 0.8);
            --accent-cyan: #00ffcc;
            --accent-pink: #ff0055;
            --accent-purple: #b000ff;
            --accent-yellow: #00e5ff;
            --border-glow: rgba(255, 0, 85, 0.5);
        }

        * {
            box-sizing: border-box;
            user-select: none;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            font-family: 'Outfit', 'Segoe UI', Roboto, sans-serif;
            background: var(--bg-gradient);
            color: var(--text-main);
            transition: background 0.5s ease;
        }

        /* Floating Background Shapes */
        .shape {
            position: absolute;
            border-radius: 50%;
            filter: blur(90px);
            opacity: 0.35;
            z-index: 0;
            animation: float 10s infinite alternate ease-in-out;
        }
        .shape-1 { width: 350px; height: 350px; background: var(--accent-purple); top: 10%; left: 10%; }
        .shape-2 { width: 400px; height: 400px; background: var(--accent-pink); bottom: 10%; right: 10%; animation-delay: -5s; }

        @keyframes float {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(40px, 50px) rotate(180deg); }
        }

        /* Top Progress Bar */
        .progress-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.1);
            z-index: 200;
        }
        .progress-bar {
            height: 100%;
            width: 11.11%;
            background: linear-gradient(90deg, var(--accent-cyan), var(--accent-pink));
            box-shadow: 0 0 12px var(--accent-cyan);
            transition: width 0.4s ease;
        }

        .deck-container {
            display: flex;
            width: 100vw;
            height: 100vh;
            transition: transform 0.4s cubic-bezier(0.25, 1, 0.5, 1);
            will-change: transform;
            position: relative;
            z-index: 10;
        }

        .slide {
            min-width: 100vw;
            height: 100vh;
            padding: 40px 20px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            user-select: text;
        }

        .slide-card {
            max-width: 920px;
            width: 100%;
            max-height: 82vh;
            overflow-y: auto;
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            border: 2px solid var(--border-glow);
            border-radius: 28px;
            padding: 45px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6), inset 0 0 20px rgba(255, 255, 255, 0.05);
            transition: border-color 0.4s ease, transform 0.3s ease;
        }

        .slide-card:hover {
            border-color: var(--accent-pink);
        }

        .slide-card::-webkit-scrollbar { width: 6px; }
        .slide-card::-webkit-scrollbar-thumb {
            background: var(--accent-pink);
            border-radius: 10px;
        }

        /* Typography & Badges */
        .badge {
            display: inline-block;
            background: linear-gradient(135deg, var(--accent-purple), var(--accent-pink));
            color: #fff;
            padding: 8px 18px;
            border-radius: 30px;
            font-size: 0.85rem;
            font-weight: 800;
            letter-spacing: 1.5px;
            text-transform: uppercase;
            margin-bottom: 18px;
            box-shadow: 0 4px 15px rgba(255, 0, 127, 0.4);
        }

        h1 {
            font-size: 2.5rem;
            margin-top: 0;
            background: linear-gradient(90deg, #ffffff, var(--accent-cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            line-height: 1.2;
        }

        h2 {
            font-size: 1.6rem;
            color: var(--accent-cyan);
            border-bottom: 2px dashed rgba(255, 255, 255, 0.15);
            padding-bottom: 12px;
            margin-top: 0;
        }

        p, li {
            font-size: 1.08rem;
            line-height: 1.65;
            color: var(--text-main);
        }

        ul, ol { padding-left: 22px; }
        li { margin-bottom: 10px; }

        /* Interactive Source Accordions for Slide 5 */
        .accordion-item {
            background: rgba(15, 23, 42, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 14px;
            margin-bottom: 12px;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .accordion-header {
            padding: 14px 18px;
            font-weight: bold;
            color: var(--accent-cyan);
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(255, 255, 255, 0.03);
        }

        .accordion-header:hover {
            background: rgba(0, 242, 254, 0.1);
        }

        .accordion-content {
            max-height: 0;
            overflow: hidden;
            padding: 0 18px;
            transition: max-height 0.3s ease, padding 0.3s ease;
            font-size: 0.98rem;
            color: var(--text-main);
        }

        .accordion-item.active .accordion-content {
            max-height: 200px;
            padding: 14px 18px;
        }

        .accordion-item.active {
            border-color: var(--accent-pink);
            box-shadow: 0 0 15px rgba(255, 0, 127, 0.2);
        }

        /* Interactive Framework Flowchart */
        .interactive-flow {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin: 20px 0;
        }

        .flow-step {
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--accent-cyan);
            padding: 14px;
            border-radius: 14px;
            text-align: center;
            font-weight: bold;
            color: var(--accent-cyan);
            transition: transform 0.3s, background 0.3s;
        }

        .flow-step:hover {
            transform: scale(1.02);
            background: rgba(0, 242, 254, 0.15);
        }

        .flow-arrow {
            text-align: center;
            color: var(--accent-pink);
            font-size: 1.4rem;
            font-weight: bold;
        }

        /* Navigation & Controls */
        .controls {
            position: fixed;
            bottom: 25px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            align-items: center;
            gap: 18px;
            background: rgba(11, 15, 25, 0.9);
            border: 2px solid var(--border-glow);
            padding: 8px 24px;
            border-radius: 40px;
            backdrop-filter: blur(15px);
            z-index: 100;
            box-shadow: 0 10px 30px rgba(0,0,0,0.8);
        }

        .nav-btn, .theme-btn {
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-pink));
            color: #000;
            border: none;
            width: 42px;
            height: 42px;
            border-radius: 50%;
            cursor: pointer;
            font-weight: 900;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .nav-btn:hover:not(:disabled), .theme-btn:hover {
            transform: scale(1.15) rotate(5deg);
            box-shadow: 0 0 15px var(--accent-cyan);
        }

        .nav-btn:disabled {
            opacity: 0.2;
            cursor: not-allowed;
        }

        .counter {
            font-weight: 800;
            color: var(--text-main);
            letter-spacing: 1.5px;
            font-size: 1.05rem;
        }
    </style>
</head>
<body>

    <!-- Background Animated Shapes -->
    <div class="shape shape-1"></div>
    <div class="shape shape-2"></div>

    <!-- Top Progress Bar -->
    <div class="progress-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <div class="deck-container" id="deck">

        <!-- SLIDE 1: Title -->
        <div class="slide">
            <div class="slide-card" style="text-align: center;">
                <span class="badge">🚀 PLS210 Interactive Proposal</span>
                <h1>Understanding Radical Feminism in a Hybrid Institutional Context</h1>
                <p>An Interpretivist Study of Theoretical Literacy, Lived Emotional Experience, and Social Stigma Among Female Nazarbayev University Students</p>
                <div style="margin-top: 35px; background: rgba(255,255,255,0.05); padding: 18px; border-radius: 18px; display: inline-block;">
                    <p style="margin: 5px 0;">Pseudonym: <strong style="color: var(--accent-cyan);">Winsomy546</strong></p>
                    <p style="margin: 5px 0;">Epistemological Stance: <strong style="color: var(--accent-pink);">Interpretivism</strong></p>
                </div>
                <p style="font-size: 0.9rem; color: var(--accent-yellow); margin-top: 30px; font-weight: bold;">✨ Swipe, click accordion cards, or use Keyboard Arrow Keys to Navigate ✨</p>
            </div>
        </div>

        <!-- SLIDE 2: Research Question -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">1. Research Question</span>
                <h2>Empirical Research Question</h2>
                <p><strong>Primary Question:</strong> How do female undergraduate students at Nazarbayev University (NU) in Astana understand, define, and emotionally experience the concept of <em>radical feminism</em>, and how do they navigate the tension between a Western-style liberal academic space and the traditional, conservative discourses of their home environments?</p>
                <ul>
                    <li><strong>Empirical Focus:</strong> Investigates subjective meanings and emotional experiences—strictly avoiding normative judgments (evaluating whether feminism is "good" or "bad").</li>
                    <li><strong>Scoped Population & Context:</strong> Female undergraduate students at Nazarbayev University in Astana, Kazakhstan (2025–2026).</li>
                    <li><strong>Answerability:</strong> Addressed through qualitative 1-on-1 semi-structured interviews designed to explore personal meanings and social perceptions without imposing rigid classifications.</li>
                </ul>
            </div>
        </div>

        <!-- SLIDE 3: Epistemological Positioning -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">2. Epistemology</span>
                <h2>Positioning: Interpretivism</h2>
                <p><strong>Justification over Positivism:</strong> A positivist approach (testing hypotheses via quantitative surveys) would reduce students' complex perceptions to static variables and numerical "literacy" scores. However, concepts like <em>radical feminism</em>, <em>misandry</em>, and <em>tradition</em> are socially constructed and emotionally charged.</p>
                <p>Interpretivism allows the researcher to maintain <strong>epistemic openness</strong> (Ackerly & True, 2010)[cite: 1]. Participants' lived experiences, contradictions, and unexpected views are not treated as "statistical noise," but as the core data needed to understand how meaning is constructed within a hybrid space[cite: 1].</p>
            </div>
        </div>

        <!-- SLIDE 4: Contribution -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">3. Contribution</span>
                <h2>Scholarly Contribution & Gap</h2>
                <p>Existing literature on gender dynamics in Central Asia primarily focuses on post-Soviet retraditionalization (Tlostanova, 2010) or public responses to street activism (Udod, 2018)[cite: 2].</p>
                <p><strong>Our Contribution:</strong> This study addresses a specific empirical gap by examining how young women navigate a <strong>hybrid institutional crossroad</strong>—a Westernized academic university embedded within a society with strong patriarchal and conservative family norms[cite: 2]. It demonstrates how academic literacy can serve as a "buffer" against mediated social stigmas.</p>
            </div>
        </div>

        <!-- SLIDE 5: Literature Review (Interactive Accordion) -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">4. Literature Review</span>
                <h2>6 Key Academic Sources <span style="font-size: 0.8rem; color: var(--accent-yellow);">(Click to expand)</span></h2>
                
                <div class="accordion-item active" onclick="toggleAccordion(this)">
                    <div class="accordion-header">
                        <span>1. Ackerly & True (2010) — Doing Feminist Research</span>
                        <span>▼</span>
                    </div>
                    <div class="accordion-content">
                        Methodological foundation. Establishes the "Feminist Research Ethic" (attentiveness to power dynamics, reflexivity, marginalized voices) and "Feminist Accountability"[cite: 1].
                    </div>
                </div>

                <div class="accordion-item" onclick="toggleAccordion(this)">
                    <div class="accordion-header">
                        <span>2. Udod (2018) — Feminisms in Kazakhstan (NU Repository)</span>
                        <span>▼</span>
                    </div>
                    <div class="accordion-content">
                        Direct empirical precedence at NU. Analyzes "tangled ideological layers" (traditional patriarchy, Soviet legacy, Western neoliberalism) and post-socialist feminist development[cite: 2].
                    </div>
                </div>

                <div class="accordion-item" onclick="toggleAccordion(this)">
                    <div class="accordion-header">
                        <span>3. Tlostanova (2010) — Gender Epistemologies</span>
                        <span>▼</span>
                    </div>
                    <div class="accordion-content">
                        Theoretical lens of "double coloniality" (Russian imperialism + global neoliberalism) and "border thinking" as a third path beyond binary choices.
                    </div>
                </div>

                <div class="accordion-item" onclick="toggleAccordion(this)">
                    <div class="accordion-header">
                        <span>4. Mendes (2011) — Framing Feminism</span>
                        <span>▼</span>
                    </div>
                    <div class="accordion-content">
                        Critical discourse analysis revealing the "sanitization of radical ideas" and media binaries between "sensible liberals" and "deviant/hysterical radicals".
                    </div>
                </div>

                <div class="accordion-item" onclick="toggleAccordion(this)">
                    <div class="accordion-header">
                        <span>5. MacKinnon (1989) — Toward a Feminist Theory of the State</span>
                        <span>▼</span>
                    </div>
                    <div class="accordion-content">
                        Core radical feminist theory: sexuality as the locus of power, exposing the modern liberal state's "neutrality" as an expression of male power.
                    </div>
                </div>

                <div class="accordion-item" onclick="toggleAccordion(this)">
                    <div class="accordion-header">
                        <span>6. Journal of Gender Studies (2025) — '6B4T' Digital Feminism</span>
                        <span>▼</span>
                    </div>
                    <div class="accordion-content">
                        Analyzes confrontational digital activism (East Asian 6B4T non-cooperation movement) and how social media algorithms amplify anti-feminist backlash.
                    </div>
                </div>
            </div>
        </div>

        <!-- SLIDE 6: Analytical Framework -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">5. Analytical Framework</span>
                <h2>Sensitizing Propositions & Visual Flow</h2>
                <p>Rather than rigid positivist hypotheses ($X \rightarrow Y$), this interpretivist study utilizes three inductive propositions for thematic coding:</p>
                
                <div class="interactive-flow">
                    <div class="flow-step">
                        P1: Peer Discourse + Traditional Norms + Social Media Algorithms (Mendes, 2011; JGS, 2025)
                    </div>
                    <div class="flow-arrow">↓</div>
                    <div class="flow-step" style="border-color: var(--accent-pink); color: var(--accent-pink);">
                        P2: Media Stereotypes Filtered through NU Academic Literacy (MacKinnon, 1989)
                    </div>
                    <div class="flow-arrow">↓</div>
                    <div class="flow-step" style="border-color: var(--accent-yellow); color: var(--accent-yellow);">
                        P3: Lived Identity Friction & Subjective Sense-Making (Udod, 2018; Tlostanova, 2010)[cite: 2]
                    </div>
                </div>
            </div>
        </div>

        <!-- SLIDE 7: Positionality Statement -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">5B. Positionality</span>
                <h2>Researcher Positionality Statement</h2>
                <p>As a fellow NU student, I hold an <strong>insider status</strong> within this community. This shared identity fosters high trust during in-depth interviews, mitigating social desirability bias when discussing sensitive topics like family pressures, misandry, or radical tactics[cite: 1].</p>
                <p><strong>Reflexivity:</strong> I recognize that my own training in political science could tempt me to evaluate participants' responses against "textbook" definitions. To counter this bias, I employ inductive coding, maintain reflexivity journals, and apply Ackerly & True's (2010) feminist research ethics to ensure participants' voices are authentically represented[cite: 1].</p>
            </div>
        </div>

        <!-- SLIDE 8: AI Transparency Statement -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">6. AI Transparency</span>
                <h2>AI Transparency Statement (~30 sec)</h2>
                <p>In developing this research proposal and slide deck, I used generative AI (Gemini) as an interactive thought partner. The AI was utilized for:</p>
                <ol>
                    <li>Refining the empirical focus and scoping of the research question.</li>
                    <li>Comparing positivist hypotheses against interpretivist sensitizing propositions.</li>
                    <li>Structuring and formatting the literature review across the 6 provided sources[cite: 1, 2].</li>
                </ol>
                <p>All source citations, theoretical frameworks, and conceptual decisions were independently verified by me using primary academic literature and the NU institutional repository (NUR)[cite: 2]. The proposal reflects my original academic voice.</p>
            </div>
        </div>

        <!-- SLIDE 9: Ungraded Reflection -->
        <div class="slide">
            <div class="slide-card">
                <span class="badge">7. Self-Reflection (Ungraded)</span>
                <h2>What Working with AI Helped Me Understand, and What Remains Unclear</h2>
                <p><strong>What I Understood:</strong> Collaborating with AI helped me realize why my study requires an <em>interpretivist paradigm</em>[cite: 1]. I initially struggled with drafting a positivist causal hypothesis, but realized that forcing human lived experiences into "X causes Y" variables distorts reality. Sensitizing propositions give me the flexibility to remain open to unexpected themes during fieldwork[cite: 1].</p>
                <p><strong>What Remains Unclear:</strong> I am still figuring out how to balance using theories from my reading to guide my study without accidentally letting those theories bias or influence how I interpret what participants tell me in their interviews[cite: 1].</p>
            </div>
        </div>

    </div>

    <!-- UI Controls -->
    <div class="controls">
        <button class="nav-btn" id="prevBtn" onclick="prevSlide()">&lt;</button>
        <span class="counter" id="counter">1 / 9</span>
        <button class="nav-btn" id="nextBtn" onclick="nextSlide()">&gt;</button>
        <button class="theme-btn" onclick="toggleTheme()" title="Switch Theme">🎨</button>
    </div>

    <script>
        let currentSlide = 0;
        const slides = document.querySelectorAll('.slide');
        const totalSlides = slides.length;
        const deck = document.getElementById('deck');
        const counter = document.getElementById('counter');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const progressBar = document.getElementById('progressBar');

        function updateSlide() {
            deck.style.transform = `translateX(-${currentSlide * 100}vw)`;
            counter.innerText = `${currentSlide + 1} / ${totalSlides}`;
            
            // Update Progress Bar
            const progress = ((currentSlide + 1) / totalSlides) * 100;
            progressBar.style.width = `${progress}%`;

            prevBtn.disabled = currentSlide === 0;
            nextBtn.disabled = currentSlide === totalSlides - 1;
        }

        function nextSlide() {
            if (currentSlide < totalSlides - 1) {
                currentSlide++;
                updateSlide();
            }
        }

        function prevSlide() {
            if (currentSlide > 0) {
                currentSlide--;
                updateSlide();
            }
        }

        function toggleTheme() {
            document.body.classList.toggle('cyber-theme');
        }

        function toggleAccordion(element) {
            element.classList.toggle('active');
        }

        // Keyboard Navigation
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowRight' || e.key === 'Space') {
                nextSlide();
            } else if (e.key === 'ArrowLeft') {
                prevSlide();
            }
        });

        // Touch/Swipe Logic
        let touchStartX = 0;
        let touchEndX = 0;

        document.addEventListener('touchstart', (e) => {
            touchStartX = e.changedTouches[0].screenX;
        }, false);

        document.addEventListener('touchend', (e) => {
            touchEndX = e.changedTouches[0].screenX;
            handleSwipe();
        }, false);

        function handleSwipe() {
            const threshold = 50;
            if (touchStartX - touchEndX > threshold) {
                nextSlide();
            }
            if (touchEndX - touchStartX > threshold) {
                prevSlide();
            }
        }

        updateSlide();
    </script>
</body>
</html>
