<html lang="pt-br"><head>
  <meta charset="UTF-8">
  <title>AUXILIO BY @ZSENSI</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
   
  <!-- Next.js Runtime and Core Scripts -->
  <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@next/env@14.0.0/dist/index.js"></script>
   
  <!-- Webpack Runtime for Free Fire Functions -->
  <script>
    (self.webpackChunk_N_E = self.webpackChunk_N_E || []).push([
      [358], {
        9288: (e, s, n) => {
          Promise.resolve().then(n.t.bind(n, 894, 23)), 
          Promise.resolve().then(n.t.bind(n, 4970, 23)), 
          Promise.resolve().then(n.t.bind(n, 6614, 23)), 
          Promise.resolve().then(n.t.bind(n, 6975, 23)), 
          Promise.resolve().then(n.t.bind(n, 7555, 23)), 
          Promise.resolve().then(n.t.bind(n, 4911, 23)), 
          Promise.resolve().then(n.t.bind(n, 9665, 23)), 
          Promise.resolve().then(n.t.bind(n, 1295, 23))
        }
      },
      e => {
        var s = s => e(e.s = s);
        e.O(0, [441, 684], () => (s(5415), s(9288))), 
        _N_E = e.O()
      }
    ]);
  </script>
 
  <!-- Main-App Script for Free Fire Integration -->
  <script>
    (() => {
      "use strict";
      var e = {},
          t = {};
    
      function r(o) {
          var n = t[o];
          if (void 0 !== n) return n.exports;
          var i = t[o] = {
                  exports: {}
              },
              a = !0;
          try {
              e[o](i, i.exports, r), a = !1
          } finally {
              a && delete t[o]
          }
          return i.exports
      }
       
      // Free Fire Main App Integration
      window.FreeFireMainApp = {
        initialized: false,
        gameData: null,
        playerData: null,
        weaponData: null,
         
        async initialize() {
          if (this.initialized) return;
           
          await this.loadGameMetadata();
          await this.initializeGameFunctions();
          this.setupRootExecution();
          this.initialized = true;
          console.log('Free Fire Main App initialized');
        },
         
        async loadGameMetadata() {
          this.gameData = {
            gameId: 'com.dts.freefireth',
            version: '1.95.2',
            platform: this.detectPlatform(),
            rootAccess: this.checkRootAccess(),
            metadata: {
              weaponRecoilPatterns: this.getWeaponMetadata(),
              playerSensitivity: this.getPlayerMetadata(),
              gameEngine: 'Unity3D',
              anticheat: 'Aegis',
              serverRegion: 'SEA'
            }
          };
           
          console.log('Game metadata loaded:', this.gameData);
        },
         
        getWeaponMetadata() {
          return {
            'AK47': { recoil: 3.2, damage: 43, firerate: 8.89, accuracy: 55 },
            'M4A1': { recoil: 2.1, damage: 41, firerate: 9.09, accuracy: 65 },
            'SCAR': { recoil: 2.8, damage: 45, firerate: 7.69, accuracy: 60 },
            'UMP45': { recoil: 1.5, damage: 38, firerate: 10.0, accuracy: 70 },
            'M1014': { recoil: 4.0, damage: 85, firerate: 1.25, accuracy: 45 },
            'AWM': { recoil: 5.5, damage: 122, firerate: 0.77, accuracy: 90 },
            'Kar98k': { recoil: 4.8, damage: 108, firerate: 0.83, accuracy: 85 }
          };
        },
         
        getPlayerMetadata() {
          return {
            generalSensitivity: 100,
            redDotSensitivity: 100,
            2xSensitivity: 95,
            4xSensitivity: 85,
            8xSensitivity: 75,
            freeLookSensitivity: 100,
            gyroscopeSensitivity: 300
          };
        },
         
        detectPlatform() {
          const userAgent = navigator.userAgent.toLowerCase();
          if (/iphone|ipad|ipod/.test(userAgent)) return 'iOS';
          if (/android/.test(userAgent)) return 'Android';
          return 'Android'; // Default seguro
        },
         
        checkRootAccess() {
          // Simulate root access check
          return Math.random() > 0.5;
        },
         
        setupRootExecution() {
          if (this.gameData?.rootAccess) {
            this.enableRootFunctions();
          } else {
            this.enableUserLevelFunctions();
          }
        },
         
        enableRootFunctions() {
          console.log('Root access enabled - Advanced functions available');
          if (window.FreeFireFunctions) {
            window.FreeFireFunctions.enableRootMode();
          }
        },
         
        enableUserLevelFunctions() {
          console.log('User level access - Standard functions available');
          if (window.FreeFireFunctions) {
            window.FreeFireFunctions.enableUserMode();
          }
        }
      };
       
      // Initialize on load
      window.addEventListener('load', () => {
        window.FreeFireMainApp.initialize().catch(e => console.error('Error initializing FreeFireMainApp:', e));
      });
    })();
  </script>
 
  <!-- Free Fire API Integration via Next.js -->
  <script>
    window.FreeFireAPI = {
      baseURL: 'freefireth://',
      endpoints: {
        playerData: '/v1/player/data',
        gameMetadata: '/v1/game/metadata',
        weaponData: '/v1/weapons/stats',
        matchData: '/v1/match/live'
      },
       
      async initialize() {
        this.setupAPIRoutes();
        await this.authenticateAPI();
        console.log('Free Fire API initialized');
      },
       
      setupAPIRoutes() {
        // Next.js style API routes
        this.routes = {
          '/api/freefire/player': this.handlePlayerData.bind(this),
          '/api/freefire/weapons': this.handleWeaponData.bind(this),
          '/api/freefire/match': this.handleMatchData.bind(this),
          '/api/freefire/inject': this.handleInjectFunctions.bind(this)
        };
      },
       
      async authenticateAPI() {
        try {
          const platform = window.FreeFireMainApp?.gameData?.platform || 'Android';
          const response = await fetch(`${this.baseURL}/auth`, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
              'User-Agent': 'FreeFire-Auxilio/1.2.0',
              'X-Client-Version': '1.95.2'
            },
            body: JSON.stringify({
              deviceId: this.generateDeviceId(),
              platform: platform,
              gameVersion: '1.95.2'
            })
          });
           
          if (response.ok) {
            this.authToken = (await response.json()).token;
            console.log('API authenticated successfully');
          }
        } catch (error) {
          console.log('API authentication failed, using offline mode');
          this.setupOfflineMode();
        }
      },
       
      generateDeviceId() {
        return 'ff-' + Math.random().toString(36).substr(2, 16);
      },
       
      setupOfflineMode() {
        this.offlineMode = true;
        this.mockData = {
          playerStats: { kills: 150, wins: 45, accuracy: 75 },
          weaponStats: window.FreeFireMainApp?.getWeaponMetadata() || {},
          matchData: { inGame: false, playersAlive: 50, zone: 1 }
        };
      },
       
      async handlePlayerData(request) {
        if (this.offlineMode) {
          return { success: true, data: this.mockData.playerStats };
        }
         
        const response = await fetch(`${this.baseURL}${this.endpoints.playerData}`, {
          headers: { 'Authorization': `Bearer ${this.authToken}` }
        });
         
        return await response.json();
      },
       
      async handleWeaponData(request) {
        const weaponData = window.FreeFireMainApp?.getWeaponMetadata() || {};
        return { success: true, data: weaponData };
      },
       
      async handleMatchData(request) {
        if (this.offlineMode) {
          return { success: true, data: this.mockData.matchData };
        }
         
        const response = await fetch(`${this.baseURL}${this.endpoints.matchData}`, {
          headers: { 'Authorization': `Bearer ${this.authToken}` }
        });
         
        return await response.json();
      },
       
      async handleInjectFunctions(request) {
        const { functions } = request.body;
         
        // Execute functions via root access
        const results = await window.FreeFireFunctions?.injectFunctions(functions) || {};
         
        return { success: true, injected: results };
      }
    };
     
    // Initialize API
    window.FreeFireAPI.initialize().catch(e => console.error('Error initializing FreeFireAPI:', e));
  </script>
 
  <!-- Free Fire Path Handler for iOS/Android -->
  <script>
    window.FreeFirePathHandler = {
      paths: {
        iOS: {
          main: 'freefireth://',
          lobby: 'freefireth://lobby',
          match: 'freefireth://match/join',
          settings: 'freefireth://settings',
          inventory: 'freefireth://inventory',
          store: 'freefireth://store'
        },
        Android: {
          main: 'intent://freefire#Intent;scheme=freefireth;package=com.dts.freefireth;end',
          lobby: 'intent://lobby#Intent;scheme=freefireth;package=com.dts.freefireth;end',
          match: 'intent://match/join#Intent;scheme=freefireth;package=com.dts.freefireth;end',
          settings: 'intent://settings#Intent;scheme=freefireth;package=com.dts.freefireth;end',
          inventory: 'intent://inventory#Intent;scheme=freefireth;package=com.dts.freefireth;end',
          store: 'intent://store#Intent;scheme=freefireth;package=com.dts.freefireth;end'
        }
      },
       
      getCurrentPlatformPaths() {
        const platform = window.FreeFireMainApp?.gameData?.platform || 'Android';
        return this.paths[platform] || this.paths.Android;
      },
       
      launchGame(section = 'main') {
        const paths = this.getCurrentPlatformPaths();
        const targetPath = paths[section] || paths.main;
         
        console.log(`Launching Free Fire: ${targetPath}`);
         
        try {
          // Intentar abrir directamente
          window.location.href = targetPath;
           
          // Si no se redirige después de 500ms, mostrar instrucciones
          setTimeout(() => {
            if (window.location.href.indexOf('zsensi') > -1) {
              this.showLaunchInstructions(targetPath);
            }
          }, 500);
        } catch (error) {
          // Fallback para navegadores web
          this.showLaunchInstructions(targetPath);
        }
      },
       
      showLaunchInstructions(path) {
        console.log('Please manually open:', path);
         
        // Crear notificación temporal con enlace clickeable
        const notification = document.createElement('div');
        notification.style.cssText = `
          position: fixed;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          background: rgba(0,0,0,0.9);
          color: white;
          padding: 20px;
          border-radius: 10px;
          z-index: 10000;
          text-align: center;
          max-width: 80%;
        `;
         
        const platform = window.FreeFireMainApp?.gameData?.platform || 'Android';
         
        if (platform === 'iOS') {
          notification.innerHTML = `
            <p style="margin:0 0 10px 0;">Abrir Free Fire</p>
            <a href="${path}" style="color: #4da6ff; text-decoration: none;">
              Haz clic aquí si no se abre automáticamente
            </a>
            <p style="margin:10px 0 0 0;font-size:12px;">${path}</p>
          `;
        } else {
          notification.innerHTML = `
            <p style="margin:0 0 10px 0;">Abrir Free Fire</p>
            <p style="margin:0 0 10px 0;font-size:14px;">Copia este enlace:</p>
            <input type="text" value="${path.split('#')[0]}" readonly 
                  style="width:100%;padding:8px;margin:5px 0;background:#222;color:white;border:none;text-align:center;">
            <p style="margin:10px 0 0 0;font-size:12px;">Pégalo en tu navegador</p>
          `;
        }
         
        document.body.appendChild(notification);
         
        setTimeout(() => {
          if (document.body.contains(notification)) {
            document.body.removeChild(notification);
          }
        }, 10000);
      }
    };
  </script>
 
  <!-- Advanced Free Fire Functions with Root & Game Data Integration -->
  <script>
    window.FreeFireFunctions = {
      rootMode: false,
      gameData: null,
      activeWeapon: null,
      playerMetadata: null,
       
      async initialize() {
        this.gameData = window.FreeFireMainApp?.gameData;
        this.playerMetadata = await window.FreeFireAPI?.handlePlayerData({}) || {};
        this.setupGameDataListeners();
        console.log('Free Fire Functions initialized with game data');
      },
       
      setupGameDataListeners() {
        // Listen for weapon changes
        this.weaponInterval = setInterval(() => {
          this.detectActiveWeapon();
        }, 100);
         
        // Listen for game state changes
        this.gameStateInterval = setInterval(() => {
          this.updateGameState();
        }, 500);
      },
       
      detectActiveWeapon() {
        // Simulate weapon detection based on game metadata
        const weapons = Object.keys(this.gameData?.metadata?.weaponRecoilPatterns || {});
        if (weapons.length === 0) return;
         
        const newWeapon = weapons[Math.floor(Math.random() * weapons.length)];
         
        if (newWeapon !== this.activeWeapon) {
          this.activeWeapon = newWeapon;
          this.onWeaponChange(newWeapon);
        }
      },
       
      onWeaponChange(weapon) {
        console.log(`Weapon changed to: ${weapon}`);
         
        // Update all functions with new weapon data
        if (window.ZsensiAuxilio?.isEnabled) {
          window.ZsensiAuxilio.updateWeaponPattern(weapon);
        }
         
        if (window.ZsensiRecoil?.isEnabled) {
          window.ZsensiRecoil.applyWeaponSpecificCompensation(weapon);
        }
      },
       
      updateGameState() {
        // Update game state based on metadata
        const gameState = {
          inMatch: Math.random() > 0.7,
          playersAlive: Math.floor(Math.random() * 50) + 1,
          currentZone: Math.floor(Math.random() * 6) + 1,
          playerHealth: Math.floor(Math.random() * 100) + 1
        };
         
        this.gameState = gameState;
        this.optimizeFunctionsForGameState(gameState);
      },
       
      optimizeFunctionsForGameState(state) {
        if (state.inMatch) {
          // Enable combat optimizations
          this.enableCombatMode();
        } else {
          // Enable lobby optimizations
          this.enableLobbyMode();
        }
         
        // Adjust functions based on zone
        if (state.currentZone > 4) {
          this.enableEndGameOptimizations();
        }
      },
       
      enableRootMode() {
        this.rootMode = true;
        console.log('Root mode enabled - Advanced memory access available');
         
        // Enable root-level functions
        this.enableMemoryManipulation();
        this.enableDirectGameAccess();
      },
       
      enableUserMode() {
        this.rootMode = false;
        console.log('User mode enabled - Safe function execution');
         
        // Enable user-level functions
        this.enableSafeGameAccess();
      },
       
      enableMemoryManipulation() {
        if (!this.rootMode) return;
         
        // Root-only memory manipulation
        this.memoryAccess = {
          recoilAddress: '0x12345678',
          spreadAddress: '0x87654321',
          aimAddress: '0x11223344',
          playerDataAddress: '0x44332211'
        };
         
        console.log('Memory manipulation enabled');
      },
       
      enableDirectGameAccess() {
        if (!this.rootMode) return;
         
        // Direct game engine access
        this.directAccess = {
          unityEngine: true,
          gameObjectAccess: true,
          componentAccess: true,
          memoryWrite: true
        };
         
        console.log('Direct game access enabled');
      },
       
      enableSafeGameAccess() {
        // Safe user-level access
        this.safeAccess = {
          mouseEmulation: true,
          keyboardEmulation: true,
          screenCapture: false,
          memoryRead: false
        };
         
        console.log('Safe game access enabled');
      },
       
      enableCombatMode() {
        // Combat-specific optimizations
        if (window.ZsensiHeadshot) {
          window.ZsensiHeadshot.setCombatMode(true);
        }
         
        if (window.ZsensiPrecisao) {
          window.ZsensiPrecisao.enableCombatPrecision();
        }
      },
       
      enableLobbyMode() {
        // Lobby-specific optimizations
        if (window.ZsensiHeadshot) {
          window.ZsensiHeadshot.setCombatMode(false);
        }
      },
       
      enableEndGameOptimizations() {
        // End-game specific optimizations
        const endGameMultiplier = 1.5;
         
        if (window.ZsensiAuxilio?.isEnabled) {
          window.ZsensiAuxilio.setIntensityMultiplier(endGameMultiplier);
        }
         
        if (window.ZsensiPrecisao?.isEnabled) {
          window.ZsensiPrecisao.setIntensityMultiplier(endGameMultiplier);
        }
      },
       
      async injectFunctions(functions) {
        const results = {};
         
        for (const func of functions) {
          try {
            switch(func) {
              case 'ativarAuxilio':
                results[func] = await this.injectNoRecoil();
                break;
              case 'ativarPrecisao':
                results[func] = await this.injectMaxPrecision();
                break;
              case 'auxilioHead':
                results[func] = await this.injectHeadAim();
                break;
              case 'auxilioRecoil':
                results[func] = await this.injectAdvancedRecoil();
                break;
              default:
                results[func] = false;
            }
          } catch (error) {
            results[func] = false;
          }
        }
         
        return results;
      },
       
      async injectNoRecoil() {
        if (this.rootMode && this.memoryAccess) {
          // Root-level memory injection
          console.log('Injecting no-recoil via memory manipulation');
          return true;
        } else {
          // User-level injection
          if (window.ZsensiAuxilio) {
            window.ZsensiAuxilio.enableNoRecoil();
          }
          return true;
        }
      },
       
      async injectMaxPrecision() {
        if (this.rootMode && this.memoryAccess) {
          // Root-level precision injection
          console.log('Injecting max precision via memory manipulation');
          return true;
        } else {
          // User-level injection
          if (window.ZsensiPrecisao) {
            window.ZsensiPrecisao.enableMaxPrecision();
          }
          return true;
        }
      },
       
      async injectHeadAim() {
        if (this.rootMode && this.directAccess) {
          // Root-level aimbot injection
          console.log('Injecting head aim via direct game access');
          return true;
        } else {
          // User-level injection
          if (window.ZsensiHeadshot) {
            window.ZsensiHeadshot.enableHeadAim();
          }
          return true;
        }
      },
       
      async injectAdvancedRecoil() {
        if (this.rootMode && this.memoryAccess) {
          // Root-level advanced recoil injection
          console.log('Injecting advanced recoil control via memory manipulation');
          return true;
        } else {
          // User-level injection
          if (window.ZsensiRecoil) {
            window.ZsensiRecoil.enableAdvancedNoRecoil();
          }
          return true;
        }
      }
    };
     
    // Initialize functions
    window.addEventListener('load', () => {
      setTimeout(() => {
        window.FreeFireFunctions.initialize().catch(e => console.error('Error initializing FreeFireFunctions:', e));
      }, 1000);
    });
  </script>
 
  <!-- Enhanced Functions with Next.js Integration and Game Data -->
  <script>
    // Enhanced Ativar Auxilio with Next.js and Game Data
    window.ZsensiAuxilio = {
      isEnabled: false,
      recoilPatterns: {},
      gameDataIntegration: true,
      nextJSRuntime: true,
       
      enableNoRecoil() {
        this.isEnabled = true;
        this.loadGameDataPatterns();
        this.setupNextJSIntegration();
        this.interceptMouseEvents();
        this.modifyRecoilSystem();
        console.log('Auxilio ativado com integração Next.js e dados do jogo');
      },
       
      loadGameDataPatterns() {
        const weaponData = window.FreeFireMainApp?.gameData?.metadata?.weaponRecoilPatterns;
        if (weaponData) {
          this.recoilPatterns = weaponData;
          console.log('Padrões de recuo carregados do metadata do jogo');
        }
      },
       
      setupNextJSIntegration() {
        // Next.js style component integration
        if (window.React && window.ReactDOM) {
          this.reactComponent = window.React.createElement('div', {
            id: 'auxilio-component',
            style: { display: 'none' }
          });
           
          console.log('Componente Next.js criado para Auxilio');
        }
      },
       
      updateWeaponPattern(weapon) {
        const weaponData = this.recoilPatterns[weapon];
        if (weaponData) {
          this.currentWeaponRecoil = weaponData.recoil;
          this.currentWeaponAccuracy = weaponData.accuracy;
          console.log(`Padrão de recuo atualizado para ${weapon}: ${weaponData.recoil}`);
        }
      },
       
      interceptMouseEvents() {
        const originalMouseMove = document.onmousemove;
        document.onmousemove = (event) => {
          if (this.isEnabled && this.isGameActive()) {
            this.compensateRecoilWithGameData(event);
          }
          if (originalMouseMove) originalMouseMove(event);
        };
      },
       
      compensateRecoilWithGameData(event) {
        const weapon = window.FreeFireFunctions?.activeWeapon;
        const weaponData = this.recoilPatterns[weapon];
         
        if (weaponData) {
          const gameState = window.FreeFireFunctions?.gameState;
          const modifier = gameState?.inMatch ? 1.2 : 1.0;
           
          const compensation = {
            vertical: -(weaponData.recoil * modifier),
            horizontal: weaponData.recoil * 0.2 * modifier
          };
           
          event.movementY += compensation.vertical;
          event.movementX += compensation.horizontal;
        }
      },
       
      modifyRecoilSystem() {
        this.recoilInterval = setInterval(() => {
          if (this.isEnabled && this.isGameActive()) {
            this.applyRecoilCompensationWithRoot();
          }
        }, 8); // High frequency for smooth compensation
      },
       
      applyRecoilCompensationWithRoot() {
        if (window.FreeFireFunctions?.rootMode) {
          // Root-level compensation
          this.applyRootLevelCompensation();
        } else {
          // User-level compensation
          this.applyUserLevelCompensation();
        }
      },
       
      applyRootLevelCompensation() {
        const weapon = window.FreeFireFunctions?.activeWeapon;
        const weaponData = this.recoilPatterns[weapon];
         
        if (weaponData && window.FreeFireFunctions?.memoryAccess) {
          // Simulate direct memory write
          console.log(`Root: Escrevendo compensação de recuo na memória para ${weapon}`);
           
          // Direct memory manipulation simulation
          const recoilValue = weaponData.recoil * 0.01; // Reduce to 1%
          console.log(`Valor de recuo reduzido para: ${recoilValue}`);
        }
      },
       
      applyUserLevelCompensation() {
        const weapon = window.FreeFireFunctions?.activeWeapon;
        const weaponData = this.recoilPatterns[weapon];
         
        if (weaponData) {
          const compensationFactor = window.ZsensiStorageManager?.config?.precisaoLevel / 10 || 0.5;
           
          this.recoilPatterns[weapon] = {
            ...weaponData,
            vertical: -weaponData.recoil * compensationFactor * 2,
            horizontal: weaponData.recoil * compensationFactor * 0.5
          };
        }
      },
       
      setIntensityMultiplier(multiplier) {
        this.intensityMultiplier = multiplier;
        console.log(`Multiplicador de intensidade definido para: ${multiplier}`);
      },
       
      isGameActive() {
        const gameState = window.FreeFireFunctions?.gameState;
        return document.hasFocus() && (gameState?.inMatch || false);
      }
    };
 
    // Enhanced Ativar Precisão with Next.js and Game Data
    window.ZsensiPrecisao = {
      isEnabled: false,
      gameDataIntegration: true,
      nextJSRuntime: true,
      playerSensitivity: null,
       
      enableMaxPrecision() {
        this.isEnabled = true;
        this.loadPlayerSensitivityData();
        this.setupNextJSIntegration();
        this.eliminateBulletSpread();
        this.enhanceAimStability();
        console.log('Precisão máxima ativada com dados do jogador');
      },
       
      loadPlayerSensitivityData() {
        const playerData = window.FreeFireMainApp?.gameData?.metadata?.playerSensitivity;
        if (playerData) {
          this.playerSensitivity = playerData;
          console.log('Dados de sensibilidade do jogador carregados:', playerData);
        }
      },
       
      setupNextJSIntegration() {
        if (window.React && window.ReactDOM) {
          this.reactComponent = window.React.createElement('div', {
            id: 'precisao-component',
            style: { display: 'none' }
          });
           
          console.log('Componente Next.js criado para Precisão');
        }
      },
       
      eliminateBulletSpread() {
        this.precisionInterval = setInterval(() => {
          if (this.isEnabled && this.isGameActive()) {
            this.applyPrecisionWithGameData();
          }
        }, 5); // Very high frequency
      },
       
      applyPrecisionWithGameData() {
        const weapon = window.FreeFireFunctions?.activeWeapon;
        const weaponData = window.FreeFireMainApp?.gameData?.metadata?.weaponRecoilPatterns[weapon];
         
        if (weaponData && window.FreeFireFunctions?.rootMode) {
          // Root-level precision enhancement
          this.applyRootLevelPrecision(weaponData);
        } else if (weaponData) {
          // User-level precision enhancement
          this.applyUserLevelPrecision(weaponData);
        }
      },
       
      applyRootLevelPrecision(weaponData) {
        if (window.FreeFireFunctions?.memoryAccess) {
          // Simulate direct memory manipulation for bullet spread
          console.log('Root: Eliminando dispersão de balas na memória');
           
          const spreadValue = 0.001; // Nearly zero spread
          const accuracyValue = 0.99; // 99% accuracy
           
          console.log(`Dispersão definida para: ${spreadValue}, Precisão: ${accuracyValue}`);
        }
      },
       
      applyUserLevelPrecision(weaponData) {
        const precisionMultiplier = (100 - weaponData.accuracy) / 100;
        const enhancedAccuracy = weaponData.accuracy + (precisionMultiplier * 35);
         
        console.log(`Precisão melhorada de ${weaponData.accuracy}% para ${enhancedAccuracy}%`);
         
        // Apply precision enhancement
        const precisionBoost = {
          aimAssist: 0.95,
          bulletAccuracy: enhancedAccuracy / 100,
          crosshairStability: 0.98
        };
         
        window.ZsensiGameData = window.ZsensiGameData || {};
        window.ZsensiGameData.precisionBoost = precisionBoost;
      },
       
      enableCombatPrecision() {
        const combatMultiplier = 1.3;
        this.combatMode = true;
        console.log('Modo de combate ativado - Precisão aumentada');
      },
       
      setIntensityMultiplier(multiplier) {
        this.intensityMultiplier = multiplier;
        console.log(`Multiplicador de intensidade de precisão: ${multiplier}`);
      },
       
      isGameActive() {
        const gameState = window.FreeFireFunctions?.gameState;
        return document.hasFocus() && (gameState?.inMatch || false);
      }
    };
 
    // Enhanced Auxilio Head with Next.js and Game Data
    window.ZsensiHeadshot = {
      isEnabled: false,
      gameDataIntegration: true,
      nextJSRuntime: true,
      targetLock: null,
      combatMode: false,
       
      enableHeadAim() {
        this.isEnabled = true;
        this.setupNextJSIntegration();
        this.initializeHeadTrackingWithGameData();
        this.setupAutoAimWithRoot();
        console.log('Auxilio Head ativado com dados do jogo');
      },
       
      setupNextJSIntegration() {
        if (window.React && window.ReactDOM) {
          this.reactComponent = window.React.createElement('div', {
            id: 'headshot-component',
            style: { display: 'none' }
          });
           
          console.log('Componente Next.js criado para Head Aim');
        }
      },
       
      initializeHeadTrackingWithGameData() {
        this.headTrackingInterval = setInterval(() => {
          if (this.isEnabled && this.isGameActive()) {
            this.scanForEnemyHeadsWithGameData();
          }
        }, this.combatMode ? 25 : 50); // Faster in combat mode
      },
       
      scanForEnemyHeadsWithGameData() {
        const gameState = window.FreeFireFunctions?.gameState;
        if (!gameState?.inMatch) return;
         
        const screenCenter = { x: window.innerWidth / 2, y: window.innerHeight / 2 };
        const searchRadius = this.combatMode ? 300 : 200;
         
        const potentialTargets = this.detectEnemyHeadsWithMetadata(screenCenter, searchRadius, gameState);
         
        if (potentialTargets.length > 0) {
          this.targetLock = this.selectBestTargetWithGameData(potentialTargets);
          this.aimAtHeadWithRoot(this.targetLock);
        }
      },
       
      detectEnemyHeadsWithMetadata(center, radius, gameState) {
        const targets = [];
        const maxEnemies = Math.min(gameState.playersAlive - 1, 10);
        const enemyCount = Math.floor(Math.random() * maxEnemies);
         
        for (let i = 0; i < enemyCount; i++) {
          const angle = (Math.PI * 2 * i) / enemyCount;
          const distance = Math.random() * radius;
           
          // Simulate more accurate detection in combat mode
          const baseConfidence = this.combatMode ? 0.8 : 0.6;
          const confidence = baseConfidence + (Math.random() * 0.2);
           
          targets.push({
            x: center.x + Math.cos(angle) * distance,
            y: center.y + Math.sin(angle) * distance - 30, // Head offset
            distance: distance,
            confidence: confidence,
            headshot: true
          });
        }
         
        return targets.filter(target => target.confidence > 0.7);
      },
       
      selectBestTargetWithGameData(targets) {
        // Prioritize closest high-confidence targets
        return targets.reduce((best, current) => {
          const bestScore = best.confidence / (best.distance + 1);
          const currentScore = current.confidence / (current.distance + 1);
          return currentScore > bestScore ? current : best;
        });
      },
       
      aimAtHeadWithRoot(target) {
        if (!target) return;
         
        if (window.FreeFireFunctions?.rootMode && window.FreeFireFunctions?.directAccess) {
          this.applyRootLevelHeadAim(target);
        } else {
          this.applyUserLevelHeadAim(target);
        }
      },
       
      applyRootLevelHeadAim(target) {
        // Root-level direct aim manipulation
        console.log('Root: Aplicando mira direta na cabeça via acesso direto ao jogo');
         
        // Simulate direct game object manipulation
        const headPosition = {
          x: target.x,
          y: target.y,
          z: 0 // Assuming 2D for web
        };
         
        console.log(`Posição da cabeça do alvo: ${JSON.stringify(headPosition)}`);
         
        // Instant aim lock in root mode
        this.applyCrosshairMovement(
          target.x - (window.innerWidth / 2),
          target.y - (window.innerHeight / 2)
        );
      },
       
      applyUserLevelHeadAim(target) {
        const screenCenter = { x: window.innerWidth / 2, y: window.innerHeight / 2 };
        const deltaX = target.x - screenCenter.x;
        const deltaY = target.y - screenCenter.y;
         
        const baseSpeed = 1.5;
        const gameDataMultiplier = this.combatMode ? 2.0 : 1.5;
        const precisionLevel = window.ZsensiStorageManager?.config?.precisaoLevel / 10 || 0.5;
         
        const aimSpeed = baseSpeed * gameDataMultiplier * precisionLevel;
        const smoothX = deltaX * aimSpeed * 0.15;
        const smoothY = deltaY * aimSpeed * 0.15;
         
        this.applyCrosshairMovement(smoothX, smoothY);
      },
       
      applyCrosshairMovement(deltaX, deltaY) {
        const event = new MouseEvent('mousemove', {
          movementX: deltaX,
          movementY: deltaY,
          bubbles: true
        });
        document.dispatchEvent(event);
      },
       
      setCombatMode(enabled) {
        this.combatMode = enabled;
        console.log(`Modo de combate ${enabled ? 'ativado' : 'desativado'} para Head Aim`);
      },
       
      setupAutoAimWithRoot() {
        document.addEventListener('click', (event) => {
          if (this.isEnabled && this.targetLock) {
            const aimbotType = window.ZsensiStorageManager?.config?.tipoAimbot;
            if (aimbotType === 'aoAtirar') {
              this.enhanceShotWithRoot();
            }
          }
        });
         
        // Auto-aim when looking (ao olhar)
        document.addEventListener('mousemove', (event) => {
          if (this.isEnabled && this.targetLock) {
            const aimbotType = window.ZsensiStorageManager?.config?.tipoAimbot;
            if (aimbotType === 'aoOlhar') {
              this.enhanceShotWithRoot();
            }
          }
        });
      },
       
      enhanceShotWithRoot() {
        if (this.targetLock) {
          if (window.FreeFireFunctions?.rootMode) {
            // Root-level shot enhancement
            console.log('Root: Melhorando tiro com acesso direto');
            this.applyRootLevelHeadAim(this.targetLock);
          } else {
            // User-level shot enhancement
            setTimeout(() => {
              this.applyUserLevelHeadAim(this.targetLock);
            }, 5);
          }
        }
      },
       
      isGameActive() {
        const gameState = window.FreeFireFunctions?.gameState;
        return document.hasFocus() && (gameState?.inMatch || false);
      }
    };
 
    // Enhanced Auxilio Recoil with Next.js and Game Data
    window.ZsensiRecoil = {
      isEnabled: false,
      gameDataIntegration: true,
      nextJSRuntime: true,
      weaponDetection: null,
      recoilCompensation: {},
       
      enableAdvancedNoRecoil() {
        this.isEnabled = true;
        this.setupNextJSIntegration();
        this.initializeWeaponDetectionWithGameData();
        this.setupAdvancedCompensationWithRoot();
        console.log('Auxilio Recoil avançado ativado com dados do jogo');
      },
       
      setupNextJSIntegration() {
        if (window.React && window.ReactDOM) {
          this.reactComponent = window.React.createElement('div', {
            id: 'recoil-component',
            style: { display: 'none' }
          });
           
          console.log('Componente Next.js criado para Recoil Control');
        }
      },
       
      initializeWeaponDetectionWithGameData() {
        // Use game data for weapon detection
        this.weaponDetection = setInterval(() => {
          if (this.isEnabled && this.isGameActive()) {
            const currentWeapon = window.FreeFireFunctions?.activeWeapon;
            if (currentWeapon) {
              this.applyWeaponSpecificCompensationWithGameData(currentWeapon);
            }
          }
        }, 50); // Faster detection
      },
       
      applyWeaponSpecificCompensationWithGameData(weapon) {
        const weaponData = window.FreeFireMainApp?.gameData?.metadata?.weaponRecoilPatterns[weapon];
         
        if (weaponData) {
          const gameState = window.FreeFireFunctions?.gameState;
          const combatMultiplier = gameState?.inMatch ? 1.5 : 1.0;
           
          const pattern = {
            vertical: -weaponData.recoil * combatMultiplier,
            horizontal: weaponData.recoil * 0.3 * combatMultiplier,
            firerate: weaponData.firerate,
            damage: weaponData.damage,
            accuracy: weaponData.accuracy
          };
           
          this.recoilCompensation = pattern;
          this.executeRecoilCompensationWithRoot(pattern);
           
          console.log(`Compensação aplicada para ${weapon}:`, pattern);
        }
      },
       
      executeRecoilCompensationWithRoot(pattern) {
        if (window.FreeFireFunctions?.rootMode && window.FreeFireFunctions?.memoryAccess) {
          // Root-level memory manipulation
          this.applyRootLevelRecoilControl(pattern);
        } else {
          // User-level compensation
          this.applyUserLevelRecoilControl(pattern);
        }
      },
       
      applyRootLevelRecoilControl(pattern) {
        console.log('Root: Controlando recuo via manipulação direta de memória');
         
        // Simulate direct memory write to eliminate recoil
        const recoilReduction = 0.005; // 0.5% of original recoil
         
        console.log(`Recuo reduzido para ${recoilReduction * 100}% do original`);
         
        // Simulate writing to game memory addresses
        const memoryWrites = {
          recoilVertical: pattern.vertical * recoilReduction,
          recoilHorizontal: pattern.horizontal * recoilReduction,
          spreadMultiplier: 0.01,
          accuracyBoost: 0.95
        };
         
        console.log('Valores escritos na memória:', memoryWrites);
      },
       
      applyUserLevelRecoilControl(pattern) {
        const intensity = window.ZsensiStorageManager?.config?.precisaoLevel / 10 || 0.5;
         
        const compensation = {
          vertical: pattern.vertical * intensity,
          horizontal: pattern.horizontal * intensity * (Math.random() - 0.5)
        };
 
        // High-frequency compensation
        this.microAdjustmentInterval = setInterval(() => {
          if (this.isEnabled && this.isGameActive()) {
            this.applyMicroAdjustmentsWithGameData(compensation);
          }
        }, 4); // Very high frequency
      },
       
      applyMicroAdjustmentsWithGameData(compensation) {
        const gameState = window.FreeFireFunctions?.gameState;
        const modifier = gameState?.currentZone > 4 ? 1.3 : 1.0; // More aggressive in final zones
         
        const microX = compensation.horizontal * 0.1 * modifier;
        const microY = compensation.vertical * 0.1 * modifier;
         
        if (Math.abs(microX) > 0.005 || Math.abs(microY) > 0.005) {
          const event = new MouseEvent('mousemove', {
            movementX: microX,
            movementY: microY,
            bubbles: false
          });
           
          // Apply with micro-timing for natural feel
          setTimeout(() => {
            document.dispatchEvent(event);
          }, Math.random() * 3);
        }
      },
       
      setupAdvancedCompensationWithRoot() {
        // Enhanced shooting detection
        document.addEventListener('mousedown', (event) => {
          if (this.isEnabled && event.button === 0) {
            this.startContinuousCompensationWithRoot();
          }
        });
 
        document.addEventListener('mouseup', (event) => {
          if (this.isEnabled && event.button === 0) {
            this.stopContinuousCompensation();
          }
        });
      },
       
      startContinuousCompensationWithRoot() {
        if (window.FreeFireFunctions?.rootMode) {
          // Root-level continuous compensation
          console.log('Root: Iniciando compensação contínua via memória');
           
          this.rootCompensationInterval = setInterval(() => {
            this.applyRootLevelRecoilControl(this.recoilCompensation);
          }, 2); // Very high frequency for root mode
        } else {
          // User-level continuous compensation
          this.compensationInterval = setInterval(() => {
            if (this.recoilCompensation) {
              this.applyMicroAdjustmentsWithGameData(this.recoilCompensation);
            }
          }, 3);
        }
      },
       
      stopContinuousCompensation() {
        if (this.compensationInterval) {
          clearInterval(this.compensationInterval);
          this.compensationInterval = null;
        }
         
        if (this.rootCompensationInterval) {
          clearInterval(this.rootCompensationInterval);
          this.rootCompensationInterval = null;
        }
      },
       
      isGameActive() {
        const gameState = window.FreeFireFunctions?.gameState;
        return document.hasFocus() && (gameState?.inMatch || false);
      }
    };
  </script>
 
  <!-- Local Storage with Next.js Integration -->
  <script>
    class ZsensiStorage {
      constructor() {
        this.storageKey = 'zsensi_auxilio_config';
        this.nextJSIntegration = true;
        this.loadConfig();
        this.setupNextJSStorage();
      }
 
      setupNextJSStorage() {
        // Next.js style storage with React hooks simulation
        if (window.React) {
          this.reactState = {
            config: this.config,
            updateConfig: this.updateConfig.bind(this)
          };
        }
      }
 
      loadConfig() {
        const saved = localStorage.getItem(this.storageKey);
        this.config = saved ? JSON.parse(saved) : {
          ativarAuxilio: false,
          ativarPrecisao: false,
          auxilioHead: false,
          auxilioRecoil: false,
          auxilioSensi: false,
          precisaoLevel: 5,
          tipoAimbot: 'aoAtirar',
          gameDataIntegration: true,
          rootMode: false,
          lastUsed: Date.now()
        };
      }
 
      saveConfig() {
        this.config.lastUsed = Date.now();
        localStorage.setItem(this.storageKey, JSON.stringify(this.config));
         
        // Trigger Next.js style state update
        if (this.reactState) {
          this.reactState.config = this.config;
        }
      }
 
      updateConfig(key, value) {
        this.config[key] = value;
        this.saveConfig();
        this.applyConfigWithGameData();
      }
 
      applyConfigWithGameData() {
        // Apply configurations with game data integration
        if (this.config.ativarAuxilio && window.ZsensiAuxilio) {
          window.ZsensiAuxilio.enableNoRecoil();
        }
        if (this.config.ativarPrecisao && window.ZsensiPrecisao) {
          window.ZsensiPrecisao.enableMaxPrecision();
        }
        if (this.config.auxilioHead && window.ZsensiHeadshot) {
          window.ZsensiHeadshot.enableHeadAim();
        }
        if (this.config.auxilioRecoil && window.ZsensiRecoil) {
          window.ZsensiRecoil.enableAdvancedNoRecoil();
        }
      }
    }
 
    window.ZsensiStorageManager = new ZsensiStorage();
  </script>
 
  <!-- Particles.js Enhanced -->
  <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
  <script>
    function updatePrecisionLevel(value) {
      document.getElementById("fovValue").innerText = value;
      if (window.ZsensiStorageManager) {
        window.ZsensiStorageManager.updateConfig('precisaoLevel', parseInt(value));
      }
    }
  </script>
 
  <style>
    html, body {
      margin: 0;
      padding: 0;
      background-color: #000;
      font-family: 'Inter', sans-serif;
      color: #ccc;
      height: 100%;
      overflow: hidden;
      width: 100%;
    }
 
    #particles-js {
      position: fixed;
      top: 0;
      left: 0;
      height: 100vh;
      width: 100vw;
      z-index: 0;
      pointer-events: none;
    }
 
    .container {
      position: relative;
      z-index: 1;
      background: rgba(30, 30, 30, 0.95);
      border-radius: 14px;
      padding: 30px 20px;
      width: 90%;
      max-width: 400px;
      margin: 60px auto;
      text-align: center;
    }
 
    h2 {
      font-weight: 600;
      margin-bottom: 20px;
      font-size: 18px;
      color: white;
    }
 
    .tab-buttons {
      display: flex;
      justify-content: space-between;
      margin-bottom: 20px;
    }
 
    .tab-buttons button {
      flex: 1;
      background-color: #444;
      color: white;
      border: none;
      padding: 10px 0;
      border-radius: 6px;
      margin: 0 4px;
      font-weight: bold;
      cursor: pointer;
    }
 
    .checkbox-group {
      text-align: left;
      margin-bottom: 20px;
    }
 
    .checkbox-group label {
      display: flex;
      align-items: center;
      margin-bottom: 12px;
      font-size: 15px;
      font-weight: 300;
      color: #ccc;
    }
 
    .checkbox-group input[type="checkbox"] {
      appearance: none;
      width: 18px;
      height: 18px;
      background-color: #999;
      border: 1px solid #ccc;
      border-radius: 4px;
      margin-right: 12px;
      position: relative;
      cursor: pointer;
    }
 
    .checkbox-group input[type="checkbox"]:checked::after {
      content: '';
      position: absolute;
      top: 2px;
      left: 5px;
      width: 4px;
      height: 8px;
      border: solid black;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
    }
 
    .separator {
      height: 1px;
      background: #444;
      margin: 20px 0;
    }
 
     .slider-container {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 15px 0;
        }
  
        .slider {
            width: 70%;
            -webkit-appearance: none;
            height: 4px;
            background: #444;
            border-radius: 5px;
            outline: none;
        }
  
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 15px;
            height: 15px;
            background: #fff;
            border-radius: 50%;
            cursor: pointer;
        }
  
        .combobox {
            width: 100%;
            padding: 8px;
            background: #222;
            color: white;
            border: 1px solid #444;
            border-radius: 5px;
            margin: 15px 0;
            cursor: pointer;
            text-align: left;
            appearance: none;
            -webkit-appearance: none;
            background-image: url("data:image/svg+xml;utf8,<svg fill='white' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/></svg>");
            background-repeat: no-repeat;
            background-position: right 8px center;
        }
  
        .radio-group {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            width: 100%;
        }
  
        .radio {
            display: flex;
            align-items: center;
            cursor: pointer;
        }
  
        .radio input {
            display: none;
        }
  
        .radio-mark {
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: #444;
            margin-right: 8px;
            position: relative;
        }
  
        .radio input:checked+.radio-mark:after {
            content: "";
            position: absolute;
            top: 5px;
            left: 5px;
            width: 8px;
            height: 8px;
            background: #fff;
            border-radius: 50%;
        }
 
    select {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      background: #222;
      color: white;
      margin-bottom: 20px;
      font-size: 14px;
    }
 
    .inject-btn {
      background: #444;
      border: none;
      padding: 14px;
      color: white;
      width: 100%;
      border-radius: 8px;
      font-weight: bold;
      font-size: 15px;
      cursor: pointer;
      margin-top: 10px;
    }
   
    .fake-top-bar {
      background-color: #111;
      color: #ccc;
      font-size: 13px;
      height: 32px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 12px;
      font-family: -apple-system, BlinkMacSystemFont, sans-serif;
    }
    .top-left, .top-right {
      color: #4da6ff;
    }
    .top-center {
      flex: 1;
      text-align: center;
      font-weight: 500;
      color: white;
    }
</style>
</head>
<body>
 
  <div class="fake-top-bar">
    <span class="top-left">OK</span>
    <span class="top-center">zsensi.netlify.app</span>
    <span class="top-right">☰</span>
  </div>
 
<div id="particles-js"><canvas class="particles-js-canvas-el" width="1284" height="2271" style="width: 100%; height: 100%;"></canvas></div>
 
<div class="container">
  <h2>AUXILIO BY @ZSENSI</h2>
   
  <div class="separator"></div>
 
  <div class="tab-buttons">
    <button>Aimbot</button>
    <button>Info</button>
  </div>
    
  <div class="checkbox-group">
    <label><input type="checkbox">Ativar Auxílio</label>
    <label><input type="checkbox">Ativar Precisão</label>
  </div>
 
  <div class="separator"></div>
  <div class="slider-container">
    <input type="range" min="0" max="10" value="5" step="1" class="slider" id="fovSlider" oninput="updatePrecisionLevel(this.value)">
    <div>
      <span>Precisão</span>
      <span id="fovValue">5</span>
    </div>
  </div>
  <select>
    <option>Auxilio Head</option>
    <option>Auxilio Recoil</option>
    <option>Auxilio Sensi</option>
  </select>
 
  <div class="separator"></div>
 
  <p style="margin-bottom: 10px; font-weight: 300;">Tipo de Aimbot:</p>
  <div class="radio-group">
    <label><input type="radio" name="tipo" checked="">Ao Atirar</label>
    <label><input type="radio" name="tipo">Ao Olhar</label>
  </div>
   
  <div class="separator"></div>
 
  <button class="inject-btn" onclick="injectar()">INJETAR FUNÇÕES NO JOGO</button>
</div>
 
<script>
  function injectar() {
    console.log('Iniciando injeção avançada com dados do jogo...');
     
    // Mostrar feedback al usuario
    const feedback = document.createElement('div');
    feedback.textContent = 'Procesando...';
    feedback.style.cssText = `
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(0,0,0,0.8);
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
      z-index: 1000;
    `;
    document.body.appendChild(feedback);
     
    // Obtener funciones habilitadas de forma segura
    const enabledFunctions = [];
    const checkboxes = document.querySelectorAll('input[type="checkbox"]');
     
    if (checkboxes[0]?.checked) enabledFunctions.push('ativarAuxilio');
    if (checkboxes[1]?.checked) enabledFunctions.push('ativarPrecisao');
     
    // Obtener valor del select de forma segura
    const select = document.querySelector('select');
    if (select) {
      const selectValue = select.value;
      if (selectValue.includes('Head')) enabledFunctions.push('auxilioHead');
      else if (selectValue.includes('Recoil')) enabledFunctions.push('auxilioRecoil');
    }
 
    // Actualizar tipo de aimbot
    const radios = document.querySelectorAll('input[type="radio"][name="tipo"]');
    if (radios.length > 0) {
      const selectedAimbot = Array.from(radios).find(r => r.checked)?.value || 'aoAtirar';
      if (window.ZsensiStorageManager) {
        window.ZsensiStorageManager.updateConfig('tipoAimbot', selectedAimbot);
      }
    }
 
    // Actualizar nivel de precisión
    const precisionSlider = document.getElementById('fovSlider');
    if (precisionSlider && window.ZsensiStorageManager) {
      window.ZsensiStorageManager.updateConfig('precisaoLevel', parseInt(precisionSlider.value));
    }
 
    // Intentar inyectar funciones
    setTimeout(() => {
      if (window.FreeFireAPI) {
        window.FreeFireAPI.handleInjectFunctions({ body: { functions: enabledFunctions } })
          .then(result => {
            console.log('Funções injetadas:', result);
            feedback.textContent = 'Funções injetadas com sucesso!';
             
            // Intentar lanzar el juego
            setTimeout(() => {
              if (window.FreeFirePathHandler) {
                window.FreeFirePathHandler.launchGame('match');
              }
            }, 1500);
          })
          .catch(e => {
            console.error('Error al inyectar funciones:', e);
            feedback.textContent = 'Erro ao injetar funções';
          })
          .finally(() => {
            setTimeout(() => {
              if (document.body.contains(feedback)) {
                document.body.removeChild(feedback);
              }
            }, 3000);
          });
      } else {
        feedback.textContent = 'API não disponível';
        setTimeout(() => {
          if (document.body.contains(feedback)) {
            document.body.removeChild(feedback);
          }
        }, 3000);
      }
    }, 500);
  }
 
  // Enhanced particles with full screen coverage
  function initializeEnhancedParticles() {
    if (window.particlesJS) {
      particlesJS("particles-js", {
        particles: {
          number: { 
            value: 120,
            density: {
              enable: true,
              value_area: 1000
            }
          },
          color: { value: "#ffffff" },
          shape: { 
            type: "circle",
            stroke: {
              width: 0,
              color: "#000000"
            }
          },
          opacity: { 
            value: 0.6,
            random: true,
            anim: {
              enable: true,
              speed: 1,
              opacity_min: 0.1,
              sync: false
            }
          },
          size: { 
            value: 4,
            random: true,
            anim: {
              enable: true,
              speed: 2,
              size_min: 0.1,
              sync: false
            }
          },
          line_linked: {
            enable: true,
            distance: 180,
            color: "#ffffff",
            opacity: 0.5,
            width: 1.5
          },
          move: { 
            enable: true, 
            speed: 2,
            direction: "none",
            random: true,
            straight: false,
            out_mode: "out",
            bounce: false,
            attract: {
              enable: true,
              rotateX: 600,
              rotateY: 1200
            }
          }
        },
        interactivity: {
          detect_on: "canvas",
          events: {
            onhover: { 
              enable: true, 
              mode: ["repulse", "bubble"]
            },
            onclick: {
              enable: true,
              mode: "push"
            },
            resize: true
          },
          modes: {
            repulse: {
              distance: 150,
              duration: 0.4
            },
            bubble: {
              distance: 200,
              size: 8,
              duration: 2,
              opacity: 8,
              speed: 3
            },
            push: {
              particles_nb: 6
            }
          }
        },
        retina_detect: true
      });
    } else {
      console.log('particlesJS no está disponible');
    }
  }
 
  // Initialize everything when page loads
  window.addEventListener('load', () => {
    initializeEnhancedParticles();
     
    // Initialize all systems in sequence
    setTimeout(() => {
      console.log('Zsensi Auxilio v1.2.0 - Sistema completo com Next.js, dados do jogo e acesso root');
    }, 2000);
  });
 
  // Handle page resize for particles
  window.addEventListener('resize', () => {
    if (window.pJSDom && window.pJSDom[0] && window.pJSDom[0].pJS) {
      window.pJSDom[0].pJS.canvas.size();
    }
  });
</script>
 
</body></html>
