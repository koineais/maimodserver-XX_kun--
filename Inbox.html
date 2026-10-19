# 高機能版立体操作式三次元計算端末 // 歪み補正モバイル対応版

<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>高機能立体操作式三次元計算端末</title>
    <style>
        /* 基礎画面設定 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body, html {
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: #0b0f19;
            font-family: "Helvetica Neue", Arial, "Hiragino Kaku Gothic ProN", "Hiragino Sans", Meiryo, sans-serif;

            color: #e2e8f0;
            user-select: none;
            -webkit-user-select: none;
            touch-action: none; /* 画面全体の予期せぬズレを完全ロック */
        }

        /* 主枠構造 */
        #interface-container {
            position: relative;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
        }

        /* 最上部：数式・結果表示盤（2Dバックアップ） */
        #display-panel {
            width: 100%;
            padding: 16px 24px;

            background: linear-gradient(to bottom, #0f172a, #0b0f19);
            border-bottom: 2px solid #1e293b;
            text-align: right;
            z-index: 10;
            box-shadow: 0 4px 20px rgba(0,0,0,0.5);
        }
        #sub-screen {
            font-size: 13px;
            color: #64748b;
            min-height: 18px;
            letter-spacing: 1px;
            margin-bottom: 4px;
        }
        #main-screen {
            font-size: 28px;
            font-weight: bold;
            color: #38bdf8;
            letter-spacing: 2px;
            overflow-x: auto;

            white-space: nowrap;
        }
        #main-screen::-webkit-scrollbar {
            display: none;
        }

        /* 3D空間描画画布領域 */
        #canvas-section {
            flex: 1;
            width: 100%;
            background-color: #070a12;
            position: relative;
        }

        /* 画面左上の案内テキスト */
        #guide-text {
            position: absolute;
            top: 16px;
            left: 16px;

            font-size: 11px;
            color: #64748b;
            letter-spacing: 1px;
            pointer-events: none;
            z-index: 5;
            line-height: 1.6;
            background: rgba(7, 10, 18, 0.7);
            padding: 8px 12px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
    </style>
    <!-- 三次元描画のための外部部品読み込み（許可されたCDN） -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <div id="interface-container">
        

        <!-- 二次元補助結果画面（上部） -->
        <div id="display-panel">
            <div id="sub-screen"></div>
            <div id="main-screen">０</div>
        </div>

        <!-- 3D表示領域 -->
        <div id="canvas-section">
            <div id="guide-text">
                【高機能版 操作案内】<br>
                ・立体ボタンを直接叩く（クリック／タップ）<br>
                ・電卓を回す：画面を引く（ドラッグ／スワイプ）<br>
                ※文字の歪み補正済 ／ 200ミリ秒連続打鍵ロック稼働中<br>
                【特殊機能】払：現在消去 / 弾：一字消去 / 正負：反転 / 乗：二乗
            </div>
        </div>

    </div>


    <script>
        // --- 1. 計算処理ロジック（完全英語禁止） ---
        let currentInput = "0";
        let formulaString = "";
        let isCalculated = false;

        let lastInputTime = 0;
        const INPUT_LOCK_INTERVAL = 200; // 0.2秒ロック

        const mainScreen = document.getElementById('main-screen');
        const subScreen = document.getElementById('sub-screen');

        // 全角数字から半角数字への変換マップ
        function toHalfWidthNum(str) {
            return str.replace(/[０-９]/g, s => String.fromCharCode(s.charCodeAt(0) - 0xFEE0)).replace(/．/g, '.');
        }

        // 半角数字から全角数字への変換マップ
        function toFullWidthNum(str) {

            return String(str).replace(/[0-9.]/g, s => s === '.' ? '．' : String.fromCharCode(s.charCodeAt(0) + 0xFEE0));
        }

        function pressKey(key) {
            const currentTime = Date.now();
            if (currentTime - lastInputTime < INPUT_LOCK_INTERVAL) return;
            lastInputTime = currentTime;

            triggerButtonAnimation(key);

            if (key === '消去') {
                currentInput = "0";
                formulaString = "";
                isCalculated = false;
            } else if (key === '払') {
                // 現在の入力のみをリセット (クリアエントリー)
                currentInput = "0";
            } else if (key === '弾') {
                // 一文字消去 (バックスペース)

                if (isCalculated) {
                    formulaString = "";
                    isCalculated = false;
                } else if (currentInput !== "0" && currentInput !== "計算誤り") {
                    currentInput = currentInput.slice(0, -1);
                    if (currentInput === "" || currentInput === "ー") currentInput = "0";
                }
            } else if (key === '正負') {
                // プラスマイナス反転
                if (currentInput !== "0" && currentInput !== "計算誤り") {
                    if (currentInput.startsWith('ー')) {
                        currentInput = currentInput.substring(1);
                    } else {
                        currentInput = 'ー' + currentInput;
                    }
                }
            } else if (key === '乗') {
                // 二乗計算
                if (currentInput !== "計算誤り" && currentInput !== "0") {

                    try {
                        let num = parseFloat(toHalfWidthNum(currentInput));
                        let res = num * num;
                        currentInput = toFullWidthWidthClean(res);
                        isCalculated = true;
                    } catch(e) { currentInput = "計算誤り"; }
                }
            } else if (key === '％') {
                // パーセント計算（現在の数値を100で割る）
                if (currentInput !== "計算誤り" && currentInput !== "0") {
                    try {
                        let num = parseFloat(toHalfWidthNum(currentInput));
                        let res = num / 100;
                        currentInput = toFullWidthWidthClean(res);
                    } catch(e) { currentInput = "計算誤り"; }
                }
            } else if (key === '＝') {
                if (formulaString === "" && currentInput === "0") return;
                try {

                    let calcFormula = (formulaString + currentInput)
                        .replace(/＋/g, '+').replace(/ー/g, '-').replace(/×/g, '*').replace(/÷/g, '/');
                    calcFormula = toHalfWidthNum(calcFormula);

                    let result = Function('return ' + calcFormula)();
                    subScreen.innerText = formulaString + currentInput + " ＝";
                    currentInput = toFullWidthWidthClean(result);
                    formulaString = "";
                    isCalculated = true;
                } catch (e) {
                    currentInput = "計算誤り";
                }
            } else if (['＋', 'ー', '×', '÷'].includes(key)) {
                if (isCalculated) {
                    formulaString = currentInput + " " + key + " ";
                    isCalculated = false;
                } else {
                    if (currentInput === "0" && formulaString !== "") {
                        formulaString = formulaString.slice(0, -3) + " " + key + " ";

                    } else {
                        formulaString += currentInput + " " + key + " ";
                    }
                }
                currentInput = "0";
            } else {
                // 数値および小数点入力
                if (isCalculated) {
                    currentInput = key;
                    isCalculated = false;
                } else {
                    if (currentInput === "0" && key !== '．') {
                        currentInput = key;
                    } else {
                        if (key === '．' && currentInput.includes('．')) return;
                        currentInput += key;
                    }
                }
            }

            
            mainScreen.innerText = currentInput;
            if (!isCalculated) subScreen.innerText = formulaString;

            update3DDisplayCanvas();
        }

        function toFullWidthWidthClean(num) {
            // 丸め誤差対策を含む文字列化をしてから全角へ
            let s = String(Number(num.toFixed(10))); 
            return toFullWidthNum(s);
        }


        // --- 2. Three.js による三次元立体電卓描画 ---
        const container = document.getElementById('canvas-section');
        let scene, camera, renderer, calcBoard;
        let buttonMeshMap = {}; 
        let buttonObjects = []; 


        let displayCanvas, displayCtx, displayTexture;

        let isMovingCamera = false;
        let hasMovedOrDragged = false; 
        let previousMousePosition = { x: 0, y: 0 };
        let touchStartPos = { x: 0, y: 0 };
        let rotationTargetX = -0.3;
        let rotationTargetY = 0.4;

        const raycaster = new THREE.Raycaster();
        const mouseVector = new THREE.Vector2();

        window.onload = function() {
            scene = new THREE.Scene();
            scene.background = new THREE.Color('#070a12');

            camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
            camera.position.set(0, 0, 9.5); // 拡張機能に伴い少し引く


            renderer = new THREE.WebGLRenderer({ antialias: true });
            renderer.setSize(container.clientWidth, container.clientHeight);
            renderer.shadowMap.enabled = true;
            renderer.shadowMap.type = THREE.PCFSoftShadowMap;
            container.appendChild(renderer.domElement);

            const ambientLight = new THREE.AmbientLight(0xffffff, 0.65);
            scene.add(ambientLight);

            const dirLight = new THREE.DirectionalLight(0xffffff, 0.7);
            dirLight.position.set(5, 9, 7);
            dirLight.castShadow = true;
            dirLight.shadow.mapSize.width = 1024;
            dirLight.shadow.mapSize.height = 1024;
            scene.add(dirLight);

            calcBoard = new THREE.Group();
            scene.add(calcBoard);


            // 筐体ベース（機能を増やしたため縦横サイズを最適拡張：幅4.6、縦6.8）
            const bodyGeo = new THREE.BoxGeometry(4.6, 6.8, 0.4);
            const bodyMat = new THREE.MeshStandardMaterial({ color: '#1a2333', roughness: 0.5 });
            const bodyMesh = new THREE.Mesh(bodyGeo, bodyMat);
            bodyMesh.receiveShadow = true;
            calcBoard.add(bodyMesh);

            // 3D液晶表示板
            displayCanvas = document.createElement('canvas');
            displayCanvas.width = 512;
            displayCanvas.height = 128;
            displayCtx = displayCanvas.getContext('2d');
            displayTexture = new THREE.CanvasTexture(displayCanvas);
            update3DDisplayCanvas(); 

            const dispGeo = new THREE.BoxGeometry(4.2, 1.0, 0.05);
            const dispMat = new THREE.MeshStandardMaterial({ map: displayTexture, roughness: 0.2 });
            const dispMesh = new THREE.Mesh(dispGeo, dispMat);
            dispMesh.position.set(0, 2.6, 0.21); // 上部へ配置

            calcBoard.add(dispMesh);

            // ボタン配置定義（記号、位置X、位置Y、配色）-- 5行×4列に拡張して高機能化
            const keysData = [
                ['消去', -1.5, 1.7, '#ef4444'], ['払', -0.5, 1.7, '#f59e0b'],   ['弾', 0.5, 1.7, '#64748b'],   ['÷', 1.5, 1.7, '#0ea5e9'],
                ['乗', -1.5, 1.0, '#10b981'],   ['正負', -0.5, 1.0, '#10b981'], ['％', 0.5, 1.0, '#10b981'],   ['×', 1.5, 1.0, '#0ea5e9'],
                ['７', -1.5, 0.3, '#2e3a4e'],   ['８', -0.5, 0.3, '#2e3a4e'],   ['９', 0.5, 0.3, '#2e3a4e'],   ['ー', 1.5, 0.3, '#0ea5e9'],
                ['４', -1.5, -0.4, '#2e3a4e'],  ['５', -0.5, -0.4, '#2e3a4e'],  ['６', 0.5, -0.4, '#2e3a4e'],  ['＋', 1.5, -0.4, '#0ea5e9'],
                ['１', -1.5, -1.1, '#2e3a4e'],  ['２', -0.5, -1.1, '#2e3a4e'],  ['３', 0.5, -1.1, '#2e3a4e'],  ['＝', 1.5, -1.5, '#0284c7'],
                ['０', -1.0, -1.8, '#2e3a4e'],                                  ['．', 0.5, -1.8, '#2e3a4e']
            ];

            // 立体ボタンおよび「文字歪み補正テクスチャ」の自動計算生成
            keysData.forEach(k => {
                let name = k[0];
                let bx = k[1];
                let by = k[2];
                let bcolor = k[3];


                let bw = 0.8;
                let bh = 0.5;
                if (name === '＝') { bh = 1.2; by = -1.5; } // 等号の縦サイズ最適化
                if (name === '０') { bw = 1.8; bx = -1.0; } // 零の横サイズ最適化

                // ボタン本体の立体ブロック
                const btnGeo = new THREE.BoxGeometry(bw, bh, 0.2);
                const btnMat = new THREE.MeshStandardMaterial({ color: bcolor, roughness: 0.3 });
                const btnMesh = new THREE.Mesh(btnGeo, btnMat);
                btnMesh.position.set(bx, by, 0.2);
                btnMesh.castShadow = true;
                btnMesh.receiveShadow = true;

                // 【文字が伸びるバグの完全修正ノード】
                // ボタンの物理サイズ（bw / bh）の比率に合わせて、二次元Canvasの解像度アスペクト比を完全に一致させる
                const textCanvas = document.createElement('canvas');
                const baseResolution = 128; 
                textCanvas.width = baseResolution;
                textCanvas.height = Math.round(baseResolution * (bh / bw)); // アスペクト比を物理形状と完全に同期

                
                const tCtx = textCanvas.getContext('2d');
                tCtx.fillStyle = '#ffffff';
                
                // 文字数が2文字（消去、正負など）の場合はフォントサイズを自動でスケールダウンしてはみ出し防止
                let fontSize = name.length > 1 ? Math.round(textCanvas.height * 0.45) : Math.round(textCanvas.height * 0.6);
                tCtx.font = 'bold ' + fontSize + 'px sans-serif';
                tCtx.textAlign = 'center';
                tCtx.textBaseline = 'middle';
                
                // キャンバスの中心座標へ等倍描画（これで絶対に文字が引き伸ばされて歪まなくなります）
                tCtx.fillText(name, textCanvas.width / 2, textCanvas.height / 2);

                const textTex = new THREE.CanvasTexture(textCanvas);
                
                // 前面のラベルプレート
                const labelGeo = new THREE.PlaneGeometry(bw * 0.85, bh * 0.8);
                const labelMat = new THREE.MeshBasicMaterial({ 
                    map: textTex, 

                    transparent: true, 
                    side: THREE.DoubleSide 
                });
                const labelMesh = new THREE.Mesh(labelGeo, labelMat);
                labelMesh.position.set(0, 0, 0.101); // 表面のわずか手前
                btnMesh.add(labelMesh);

                btnMesh.userData = { originalZ: 0.2, keyName: name, targetZ: 0.2 };

                calcBoard.add(btnMesh);
                buttonMeshMap[name] = btnMesh; 
                buttonObjects.push(btnMesh); 
            });

            calcBoard.rotation.x = rotationTargetX;
            calcBoard.rotation.y = rotationTargetY;

            animateLoop();
        };


        // 3D液晶表示板テクスチャの更新処理
        function update3DDisplayCanvas() {
            if (!displayCtx) return;
            
            displayCtx.fillStyle = '#090d16';
            displayCtx.fillRect(0, 0, 512, 128);

            displayCtx.strokeStyle = '#1e293b';
            displayCtx.lineWidth = 4;
            displayCtx.strokeRect(4, 4, 504, 120);

            // 上段の小文字式
            displayCtx.fillStyle = '#475569';
            displayCtx.font = '20px sans-serif';
            displayCtx.textAlign = 'right';
            let dispFormula = formulaString;
            if (isCalculated) dispFormula = subScreen.innerText;
            displayCtx.fillText(dispFormula, 490, 40);


            // 下段の大文字メイン数値
            displayCtx.fillStyle = '#38bdf8';
            displayCtx.font = 'bold 44px sans-serif';
            displayCtx.fillText(currentInput, 490, 100);

            if (displayTexture) displayTexture.needsUpdate = true;
        }

        function triggerButtonAnimation(keyName) {
            const mesh = buttonMeshMap[keyName];
            if (mesh) {
                mesh.position.z = 0.08; 
                mesh.userData.targetZ = 0.08;
                setTimeout(() => { mesh.userData.targetZ = 0.2; }, 100);
            }
        }

        function animateLoop() {
            requestAnimationFrame(animateLoop);


            calcBoard.rotation.x += (rotationTargetX - calcBoard.rotation.x) * 0.1;
            calcBoard.rotation.y += (rotationTargetY - calcBoard.rotation.y) * 0.1;

            for (let name in buttonMeshMap) {
                let mesh = buttonMeshMap[name];
                if (mesh.position.z < mesh.userData.targetZ) {
                    mesh.position.z += 0.02;
                    if (mesh.position.z > mesh.userData.targetZ) mesh.position.z = mesh.userData.targetZ;
                }
            }

            renderer.render(scene, camera);
        }

        // 光線判定による3Dボタン押下処理
        function check3DButtonHit(screenX, screenY) {
            const rect = renderer.domElement.getBoundingClientRect();
            mouseVector.x = ((screenX - rect.left) / rect.width) * 2 - 1;
            mouseVector.y = -((screenY - rect.top) / rect.height) * 2 + 1;


            raycaster.setFromCamera(mouseVector, camera);
            const intersects = raycaster.intersectObjects(buttonObjects);

            if (intersects.length > 0) {
                const hitMesh = intersects[0].object;
                if (hitMesh.userData && hitMesh.userData.keyName) {
                    pressKey(hitMesh.userData.keyName);
                    return true; 
                }
            }
            return false; 
        }

        // --- 4. 操作判定制御機能 ---
        const startAction = (screenX, screenY) => {
            isMovingCamera = true;
            hasMovedOrDragged = false;
            previousMousePosition = { x: screenX, y: screenY };
            touchStartPos = { x: screenX, y: screenY };

        };

        const moveAction = (screenX, screenY) => {
            if (!isMovingCamera) return;
            let deltaX = screenX - previousMousePosition.x;
            let deltaY = screenY - previousMousePosition.y;

            let totalDist = Math.hypot(screenX - touchStartPos.x, screenY - touchStartPos.y);
            if (totalDist > 5) hasMovedOrDragged = true;

            rotationTargetY += deltaX * 0.007;
            rotationTargetX += deltaY * 0.007;

            if (rotationTargetX > 0.3) rotationTargetX = 0.3;
            if (rotationTargetX < -1.2) rotationTargetX = -1.2;

            previousMousePosition = { x: screenX, y: screenY };
        };


        const stopAction = (e, screenX, screenY) => {
            if (!isMovingCamera) return;
            isMovingCamera = false;
            if (!hasMovedOrDragged) check3DButtonHit(screenX, screenY);
        };

        container.addEventListener('mousedown', (e) => startAction(e.clientX, e.clientY));
        window.addEventListener('mousemove', (e) => moveAction(e.clientX, e.clientY));
        container.addEventListener('mouseup', (e) => stopAction(e, e.clientX, e.clientY));

        container.addEventListener('touchstart', (e) => {
            if (e.touches.length === 1) startAction(e.touches[0].clientX, e.touches[0].clientY);
        }, { passive: false });

        container.addEventListener('touchmove', (e) => {
            if (e.touches.length === 1) moveAction(e.touches[0].clientX, e.touches[0].clientY);
        }, { passive: false });

        container.addEventListener('touchend', (e) => {

            if (e.changedTouches.length === 1) stopAction(e, e.changedTouches[0].clientX, e.changedTouches[0].clientY);
        });

        window.addEventListener('resize', () => {
            if (!camera || !renderer) return;
            camera.aspect = container.clientWidth / container.clientHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(container.clientWidth, container.clientHeight);
            update3DDisplayCanvas();
        });

        document.addEventListener('touchmove', function(e) { e.preventDefault(); }, { passive: false });
    </script>
</body>
</html>


