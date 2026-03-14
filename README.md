<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sebastian Yepes | Full Stack Developer</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Space+Grotesk:wght@300;500;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        display: ['Space Grotesk', 'sans-serif'],
                    },
                    colors: {
                        primary: '#00D9FF',
                        secondary: '#7000FF',
                        accent: '#FF006E',
                        dark: '#0a0a0f',
                        surface: 'rgba(255, 255, 255, 0.03)',
                    },
                    animation: {
                        'float': 'float 6s ease-in-out infinite',
                        'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'gradient': 'gradient 8s linear infinite',
                        'glow': 'glow 2s ease-in-out infinite alternate',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-20px)' },
                        },
                        gradient: {
                            '0%, 100%': { backgroundPosition: '0% 50%' },
                            '50%': { backgroundPosition: '100% 50%' },
                        },
                        glow: {
                            '0%': { boxShadow: '0 0 20px rgba(0, 217, 255, 0.3)' },
                            '100%': { boxShadow: '0 0 40px rgba(0, 217, 255, 0.6)' },
                        }
                    }
                }
            }
        }
    </script>
    
    <style>
        body {
            background-color: #0a0a0f;
            color: #ffffff;
            overflow-x: hidden;
        }
        
        .glass {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .glass-strong {
            background: rgba(20, 20, 30, 0.7);
            backdrop-filter: blur(30px);
            -webkit-backdrop-filter: blur(30px);
            border: 1px solid rgba(255, 255, 255, 0.15);
        }
        
        .text-gradient {
            background: linear-gradient(135deg, #00D9FF 0%, #7000FF 50%, #FF006E 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .aurora-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: 
                radial-gradient(circle at 20% 50%, rgba(112, 0, 255, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(0, 217, 255, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 40% 20%, rgba(255, 0, 110, 0.1) 0%, transparent 50%);
            filter: blur(60px);
        }
        
        .grid-pattern {
            background-image: 
                linear-gradient(rgba(255, 255, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
        }
        
        .neon-border {
            position: relative;
        }
        
        .neon-border::before {
            content: '';
            position: absolute;
            inset: -2px;
            background: linear-gradient(45deg, #00D9FF, #7000FF, #FF006E, #00D9FF);
            border-radius: inherit;
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s;
            filter: blur(8px);
        }
        
        .neon-border:hover::before {
            opacity: 0.5;
        }
        
        .skill-tag {
            transition: all 0.3s ease;
        }
        
        .skill-tag:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(0, 217, 255, 0.3);
        }
        
        .timeline-line {
            background: linear-gradient(to bottom, #00D9FF, #7000FF, transparent);
        }
        
        .stat-card {
            background: linear-gradient(135deg, rgba(255,255,255,0.05) 0%, rgba(255,255,255,0.01) 100%);
        }
        
        #canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -3;
            opacity: 0.4;
        }
        
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease;
        }
        
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }
        
        .typewriter {
            overflow: hidden;
            border-right: 3px solid #00D9FF;
            white-space: nowrap;
            animation: typing 3.5s steps(40, end), blink-caret 0.75s step-end infinite;
        }
        
        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }
        
        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: #00D9FF }
        }
    </style>
</head>
<body class="antialiased selection:bg-primary selection:text-black">

    <!-- Background Effects -->
    <div class="grid-pattern"></div>
    <div class="aurora-bg"></div>
    <div id="canvas-container"></div>

    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 glass-strong border-b border-white/10">
        <div class="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
            <div class="font-display font-bold text-2xl tracking-tighter">
                <span class="text-gradient">&lt;SY /&gt;</span>
            </div>
            
            <div class="hidden md:flex space-x-8 text-sm font-medium text-gray-300">
                <a href="#about" class="hover:text-primary transition-colors">Sobre mí</a>
                <a href="#experience" class="hover:text-primary transition-colors">Experiencia</a>
                <a href="#skills" class="hover:text-primary transition-colors">Tech Stack</a>
                <a href="#projects" class="hover:text-primary transition-colors">Proyectos</a>
                <a href="#contact" class="hover:text-primary transition-colors">Contacto</a>
            </div>

            <button onclick="document.getElementById('contact').scrollIntoView({behavior: 'smooth'})" 
                    class="px-6 py-2 rounded-full bg-white/5 border border-white/20 hover:bg-white/10 hover:border-primary/50 transition-all text-sm font-medium">
                Disponible para trabajar
            </button>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative min-h-screen flex items-center justify-center pt-20 overflow-hidden">
        <div class="max-w-7xl mx-auto px-6 grid md:grid-cols-2 gap-12 items-center">
            <div class="space-y-8 z-10">
                <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full glass text-xs font-medium text-primary border border-primary/20">
                    <span class="w-2 h-2 rounded-full bg-primary animate-pulse"></span>
                    Full Stack Developer · Medellín, Colombia 🇨🇴
                </div>
                
                <h1 class="font-display text-5xl md:text-7xl font-bold leading-tight">
                    Sebastian <br>
                    <span class="text-gradient">Yepes Padilla</span>
                </h1>
                
                <div class="h-8">
                    <p class="text-xl md:text-2xl text-gray-400 font-light typewriter" id="typewriter-text">
                        Construyendo el futuro digital...
                    </p>
                </div>
                
                <p class="text-gray-400 text-lg max-w-lg leading-relaxed">
                    Especialista en arquitecturas escalables con <span class="text-primary font-semibold">+2 años</span> de experiencia 
                    optimizando sistemas para <span class="text-primary font-semibold">+10,000 usuarios diarios</span>.
                </p>

                <div class="flex flex-wrap gap-4">
                    <a href="https://linkedin.com/in/sebastianyepes-dev" target="_blank"
                       class="group px-8 py-4 rounded-full bg-primary text-black font-semibold hover:shadow-[0_0_30px_rgba(0,217,255,0.5)] transition-all flex items-center gap-2">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
                        LinkedIn
                    </a>
                    <a href="https://ecommerce-hack-sage.vercel.app" target="_blank"
                       class="px-8 py-4 rounded-full glass border border-white/20 hover:border-primary/50 transition-all font-medium flex items-center gap-2 group">
                        Ver Portfolio
                        <svg class="w-4 h-4 group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
                    </a>
                </div>

                <div class="flex items-center gap-6 pt-4 text-sm text-gray-500">
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></div>
                        Disponible para remoto
                    </div>
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-blue-500"></div>
                        Inglés B1 Profesional
                    </div>
                </div>
            </div>

            <div class="relative hidden md:block">
                <div class="relative w-full aspect-square max-w-md mx-auto">
                    <div class="absolute inset-0 bg-gradient-to-tr from-primary/20 to-secondary/20 rounded-full blur-3xl animate-pulse-slow"></div>
                    <div class="relative glass-strong rounded-3xl p-8 transform hover:scale-105 transition-transform duration-500 border border-white/10">
                        <div class="space-y-6">
                            <div class="flex justify-between items-center border-b border-white/10 pb-4">
                                <span class="text-gray-400 text-sm">Current Role</span>
                                <span class="text-primary font-mono text-sm">Full Stack @ Quipux</span>
                            </div>
                            <div class="space-y-4">
                                <div class="flex justify-between items-center">
                                    <span class="text-gray-400">Performance</span>
                                    <span class="text-green-400 font-mono">+75% DB Speed</span>
                                </div>
                                <div class="w-full bg-white/5 rounded-full h-2">
                                    <div class="bg-gradient-to-r from-primary to-secondary h-2 rounded-full" style="width: 75%"></div>
                                </div>
                                
                                <div class="flex justify-between items-center pt-2">
                                    <span class="text-gray-400">Daily Users</span>
                                    <span class="text-primary font-mono">10K+</span>
                                </div>
                                <div class="w-full bg-white/5 rounded-full h-2">
                                    <div class="bg-gradient-to-r from-secondary to-accent h-2 rounded-full" style="width: 90%"></div>
                                </div>
                            </div>
                            
                            <div class="grid grid-cols-3 gap-2 pt-4">
                                <div class="glass rounded-lg p-3 text-center">
                                    <div class="text-2xl font-bold text-primary">2+</div>
                                    <div class="text-xs text-gray-500">Años Exp</div>
                                </div>
                                <div class="glass rounded-lg p-3 text-center">
                                    <div class="text-2xl font-bold text-secondary">95%</div>
                                    <div class="text-xs text-gray-500">Test Coverage</div>
                                </div>
                                <div class="glass rounded-lg p-3 text-center">
                                    <div class="text-2xl font-bold text-accent">40%</div>
                                    <div class="text-xs text-gray-500">Optimización</div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Floating Elements -->
                    <div class="absolute -top-4 -right-4 glass px-4 py-2 rounded-full text-xs font-mono text-primary animate-float border border-primary/20">
                        NestJS
                    </div>
                    <div class="absolute -bottom-4 -left-4 glass px-4 py-2 rounded-full text-xs font-mono text-secondary animate-float border border-secondary/20" style="animation-delay: 1s;">
                        Next.js 14
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Stats Section -->
    <section class="py-20 relative">
        <div class="max-w-7xl mx-auto px-6">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                <div class="glass rounded-2xl p-6 text-center hover:bg-white/5 transition-all reveal">
                    <div class="text-4xl font-display font-bold text-gradient mb-2">75%</div>
                    <div class="text-sm text-gray-400">Reducción Latencia DB</div>
                </div>
                <div class="glass rounded-2xl p-6 text-center hover:bg-white/5 transition-all reveal" style="transition-delay: 100ms;">
                    <div class="text-4xl font-display font-bold text-gradient mb-2">10K+</div>
                    <div class="text-sm text-gray-400">Usuarios Activos/Día</div>
                </div>
                <div class="glass rounded-2xl p-6 text-center hover:bg-white/5 transition-all reveal" style="transition-delay: 200ms;">
                    <div class="text-4xl font-display font-bold text-gradient mb-2">2+</div>
                    <div class="text-sm text-gray-400">Años Producción</div>
                </div>
                <div class="glass rounded-2xl p-6 text-center hover:bg-white/5 transition-all reveal" style="transition-delay: 300ms;">
                    <div class="text-4xl font-display font-bold text-gradient mb-2">95%</div>
                    <div class="text-sm text-gray-400">Cobertura de Tests</div>
                </div>
            </div>
        </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-20 relative">
        <div class="max-w-7xl mx-auto px-6">
            <div class="grid md:grid-cols-2 gap-16 items-center">
                <div class="reveal">
                    <h2 class="font-display text-4xl font-bold mb-6">
                        Arquitectura <span class="text-gradient">Limpia</span><br>
                        & Performance
                    </h2>
                    <div class="space-y-4 text-gray-400 leading-relaxed">
                        <p>
                            Desarrollador Full Stack con enfoque en <span class="text-white font-medium">soluciones empresariales escalables</span>. 
                            Especializado en optimización de bases de datos y arquitecturas modernas con TypeScript, 
                            Next.js y NestJS.
                        </p>
                        <p>
                            Experiencia probada en entornos ágiles entregando código production-ready con 
                            <span class="text-primary">95% de cobertura de pruebas</span>. Apasionado por la 
                            optimización de queries SQL y la creación de APIs RESTful seguras.
                        </p>
                        <p>
                            Actualmente liderando el desarrollo de aplicaciones críticas en 
                            <span class="text-white">Quipux S.A.</span>, atendiendo más de 10,000 usuarios diarios 
                            con latencias optimizadas.
                        </p>
                    </div>
                    
                    <div class="mt-8 flex gap-4">
                        <div class="flex items-center gap-2 text-sm text-gray-400">
                            <div class="w-8 h-8 rounded-full glass flex items-center justify-center text-primary">📍</div>
                            Medellín, Colombia
                        </div>
                        <div class="flex items-center gap-2 text-sm text-gray-400">
                            <div class="w-8 h-8 rounded-full glass flex items-center justify-center text-secondary">🌎</div>
                            Open to Remote
                        </div>
                    </div>
                </div>
                
                <div class="relative reveal">
                    <div class="glass-strong rounded-3xl p-8 border border-white/10">
                        <h3 class="font-display text-xl font-semibold mb-6 text-primary">Formación Continua</h3>
                        <div class="space-y-6">
                            <div class="flex gap-4">
                                <div class="w-1 bg-gradient-to-b from-primary to-transparent rounded-full"></div>
                                <div>
                                    <div class="font-semibold text-white">Tecnología en Sistemas</div>
                                    <div class="text-sm text-gray-400">IUSH · 2026 (En curso)</div>
                                </div>
                            </div>
                            <div class="flex gap-4">
                                <div class="w-1 bg-gradient-to-b from-secondary to-transparent rounded-full"></div>
                                <div>
                                    <div class="font-semibold text-white">Full Stack Node.js · React · TypeScript</div>
                                    <div class="text-sm text-gray-400">Udemy</div>
                                </div>
                            </div>
                            <div class="flex gap-4">
                                <div class="w-1 bg-gradient-to-b from-accent to-transparent rounded-full"></div>
                                <div>
                                    <div class="font-semibold text-white">Java 21 & Spring Boot</div>
                                    <div class="text-sm text-gray-400">Udemy</div>
                                </div>
                            </div>
                            <div class="flex gap-4">
                                <div class="w-1 bg-gradient-to-b from-primary to-transparent rounded-full"></div>
                                <div>
                                    <div class="font-semibold text-white">SQL con PostgreSQL</div>
                                    <div class="text-sm text-gray-400">DevTalles</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Tech Stack -->
    <section id="skills" class="py-20 relative overflow-hidden">
        <div class="max-w-7xl mx-auto px-6">
            <div class="text-center mb-16 reveal">
                <h2 class="font-display text-4xl font-bold mb-4">Tech <span class="text-gradient">Stack</span></h2>
                <p class="text-gray-400">Tecnologías modernas para aplicaciones escalables</p>
            </div>

            <div class="grid md:grid-cols-3 gap-8">
                <!-- Frontend -->
                <div class="glass rounded-2xl p-8 hover:border-primary/30 transition-all reveal group">
                    <div class="flex items-center gap-3 mb-6">
                        <div class="w-10 h-10 rounded-lg bg-primary/10 flex items-center justify-center text-primary group-hover:scale-110 transition-transform">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
                        </div>
                        <h3 class="font-display text-xl font-semibold">Frontend</h3>
                    </div>
                    <div class="flex flex-wrap gap-2">
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-primary border border-primary/20">Next.js 14</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-gray-300 border border-white/10">React</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-blue-400 border border-blue-400/20">TypeScript</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-cyan-400 border border-cyan-400/20">Tailwind CSS</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-purple-400 border border-purple-400/20">Zustand</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-red-400 border border-red-400/20">Angular</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-gray-300 border border-white/10">React Query</span>
                    </div>
                </div>

                <!-- Backend -->
                <div class="glass rounded-2xl p-8 hover:border-secondary/30 transition-all reveal group" style="transition-delay: 100ms;">
                    <div class="flex items-center gap-3 mb-6">
                        <div class="w-10 h-10 rounded-lg bg-secondary/10 flex items-center justify-center text-secondary group-hover:scale-110 transition-transform">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h14M5 12a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v4a2 2 0 01-2 2M5 12a2 2 0 01-2 2v4a2 2 0 012 2h14a2 2 0 012-2v-4a2 2 0 01-2-2m-2-4h.01M17 16h.01"/></svg>
                        </div>
                        <h3 class="font-display text-xl font-semibold">Backend</h3>
                    </div>
                    <div class="flex flex-wrap gap-2">
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-red-500 border border-red-500/20">NestJS</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-orange-400 border border-orange-400/20">Java</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-green-400 border border-green-400/20">Spring Boot</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-green-500 border border-green-500/20">Node.js</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-gray-300 border border-white/10">REST APIs</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-pink-400 border border-pink-400/20">GraphQL</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-yellow-400 border border-yellow-400/20">JWT Auth</span>
                    </div>
                </div>

                <!-- Database & DevOps -->
                <div class="glass rounded-2xl p-8 hover:border-accent/30 transition-all reveal group" style="transition-delay: 200ms;">
                    <div class="flex items-center gap-3 mb-6">
                        <div class="w-10 h-10 rounded-lg bg-accent/10 flex items-center justify-center text-accent group-hover:scale-110 transition-transform">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4m0 5c0 2.21-3.582 4-8 4s-8-1.79-8-4"/></svg>
                        </div>
                        <h3 class="font-display text-xl font-semibold">Data & DevOps</h3>
                    </div>
                    <div class="flex flex-wrap gap-2">
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-blue-500 border border-blue-500/20">PostgreSQL</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-red-600 border border-red-600/20">Oracle</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-green-500 border border-green-500/20">MongoDB</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-teal-400 border border-teal-400/20">Docker</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-orange-500 border border-orange-500/20">Git</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-gray-300 border border-white/10">CI/CD</span>
                        <span class="skill-tag px-3 py-1 rounded-full glass text-sm text-white border border-white/20">Prisma</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Experience Timeline -->
    <section id="experience" class="py-20 relative">
        <div class="max-w-5xl mx-auto px-6">
            <div class="text-center mb-16 reveal">
                <h2 class="font-display text-4xl font-bold mb-4">Experiencia <span class="text-gradient">Profesional</span></h2>
                <p class="text-gray-400">Trayectoria en desarrollo enterprise</p>
            </div>

            <div class="relative">
                <div class="absolute left-4 md:left-1/2 transform md:-translate-x-1/2 h-full w-0.5 timeline-line"></div>
                
                <!-- Experience 1 -->
                <div class="relative mb-12 reveal">
                    <div class="md:flex items-center justify-between">
                        <div class="md:w-5/12 md:text-right mb-4 md:mb-0">
                            <div class="glass rounded-2xl p-6 neon-border hover:scale-105 transition-transform">
                                <h3 class="font-display text-xl font-bold text-white mb-1">Full Stack Developer</h3>
                                <div class="text-primary font-medium mb-2">Quipux S.A.</div>
                                <div class="text-sm text-gray-400 mb-4">Feb 2024 – Presente · Medellín</div>
                                <ul class="text-sm text-gray-300 space-y-2 text-left md:text-right">
                                    <li class="flex md:justify-end gap-2">
                                        <span>Optimización DB Oracle 75%</span>
                                        <span class="text-primary">⚡</span>
                                    </li>
                                    <li class="flex md:justify-end gap-2">
                                        <span>10K+ usuarios diarios</span>
                                        <span class="text-secondary">👥</span>
                                    </li>
                                    <li class="flex md:justify-end gap-2">
                                        <span>Java Spring Boot + Next.js</span>
                                        <span class="text-accent">🚀</span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                        <div class="absolute left-4 md:left-1/2 transform -translate-x-1/2 w-4 h-4 rounded-full bg-primary border-4 border-dark z-10"></div>
                        <div class="md:w-5/12 md:pl-12 hidden md:block"></div>
                    </div>
                </div>

                <!-- Experience 2 -->
                <div class="relative reveal">
                    <div class="md:flex items-center justify-between">
                        <div class="md:w-5/12 hidden md:block"></div>
                        <div class="absolute left-4 md:left-1/2 transform -translate-x-1/2 w-4 h-4 rounded-full bg-secondary border-4 border-dark z-10"></div>
                        <div class="md:w-5/12 md:pl-12 mb-4 md:mb-0">
                            <div class="glass rounded-2xl p-6 neon-border hover:scale-105 transition-transform">
                                <h3 class="font-display text-xl font-bold text-white mb-1">Junior Developer</h3>
                                <div class="text-secondary font-medium mb-2">Quipux S.A. · Semillero</div>
                                <div class="text-sm text-gray-400 mb-4">Ene 2023 – Ene 2024</div>
                                <ul class="text-sm text-gray-300 space-y-2">
                                    <li class="flex gap-2">
                                        <span class="text-secondary">📈</span>
                                        <span>+40% mejora en respuesta SQL</span>
                                    </li>
                                    <li class="flex gap-2">
                                        <span class="text-primary">🎨</span>
                                        <span>Componentes Angular enterprise</span>
                                    </li>
                                    <li class="flex gap-2">
                                        <span class="text-accent">🔧</span>
                                        <span>POO & Clean Code Java</span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Featured Project -->
    <section id="projects" class="py-20 relative">
        <div class="max-w-7xl mx-auto px-6">
            <div class="text-center mb-16 reveal">
                <h2 class="font-display text-4xl font-bold mb-4">Proyecto <span class="text-gradient">Destacado</span></h2>
                <p class="text-gray-400">Arquitectura limpia en producción</p>
            </div>

            <div class="glass-strong rounded-3xl overflow-hidden border border-white/10 reveal">
                <div class="grid md:grid-cols-2">
                    <div class="p-8 md:p-12 flex flex-col justify-center">
                        <div class="flex items-center gap-3 mb-6">
                            <span class="px-3 py-1 rounded-full bg-primary/10 text-primary text-xs font-bold border border-primary/20">FULL STACK</span>
                            <span class="px-3 py-1 rounded-full bg-green-500/10 text-green-400 text-xs font-bold border border-green-500/20">PRODUCTION</span>
                        </div>
                        
                        <h3 class="font-display text-3xl font-bold mb-4">Ecommerce Hack 6</h3>
                        <p class="text-gray-400 mb-6 leading-relaxed">
                            Plataforma de comercio electrónico especializada en herramientas de ciberseguridad. 
                            Construida con <span class="text-white">Clean Architecture</span>, autenticación JWT 
                            segura e integración con Stripe.
                        </p>
                        
                        <div class="grid grid-cols-2 gap-4 mb-8">
                            <div class="glass rounded-lg p-4">
                                <div class="text-primary font-bold text-lg">Next.js 14</div>
                                <div class="text-xs text-gray-500">Frontend App Router</div>
                            </div>
                            <div class="glass rounded-lg p-4">
                                <div class="text-secondary font-bold text-lg">NestJS</div>
                                <div class="text-xs text-gray-500">Backend API REST</div>
                            </div>
                            <div class="glass rounded-lg p-4">
                                <div class="text-accent font-bold text-lg">PostgreSQL</div>
                                <div class="text-xs text-gray-500">Prisma ORM</div>
                            </div>
                            <div class="glass rounded-lg p-4">
                                <div class="text-yellow-400 font-bold text-lg">Stripe</div>
                                <div class="text-xs text-gray-500">Payments</div>
                            </div>
                        </div>
                        
                        <div class="flex gap-4">
                            <a href="https://ecommerce-hack-sage.vercel.app" target="_blank" 
                               class="flex-1 px-6 py-3 rounded-full bg-primary text-black font-semibold text-center hover:shadow-[0_0_30px_rgba(0,217,255,0.4)] transition-all">
                                Demo en Vivo
                            </a>
                            <a href="https://github.com/sebast219/ecommerce-hack" target="_blank"
                               class="flex-1 px-6 py-3 rounded-full glass border border-white/20 text-center hover:border-white/40 transition-all">
                                Ver Código
                            </a>
                        </div>
                    </div>
                    
                    <div class="relative bg-gradient-to-br from-primary/5 to-secondary/5 p-8 md:p-12 flex items-center justify-center">
                        <div class="relative w-full max-w-md">
                            <div class="absolute inset-0 bg-primary/20 blur-3xl rounded-full"></div>
                            <div class="relative glass rounded-2xl p-6 border border-white/10 shadow-2xl">
                                <div class="flex items-center gap-2 mb-4">
                                    <div class="w-3 h-3 rounded-full bg-red-500"></div>
                                    <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                                    <div class="w-3 h-3 rounded-full bg-green-500"></div>
                                </div>
                                <div class="space-y-3">
                                    <div class="h-2 bg-white/10 rounded w-3/4"></div>
                                    <div class="h-2 bg-white/10 rounded w-1/2"></div>
                                    <div class="h-2 bg-white/10 rounded w-5/6"></div>
                                    <div class="mt-6 glass rounded-lg p-4 border border-primary/20">
                                        <div class="flex items-center justify-between mb-2">
                                            <span class="text-xs text-primary">JWT Auth</span>
                                            <span class="text-xs text-green-400">Active</span>
                                        </div>
                                        <div class="h-1 bg-white/10 rounded-full overflow-hidden">
                                            <div class="h-full bg-primary w-full animate-pulse"></div>
                                        </div>
                                    </div>
                                    <div class="grid grid-cols-3 gap-2 mt-4">
                                        <div class="h-16 glass rounded border border-white/5"></div>
                                        <div class="h-16 glass rounded border border-white/5"></div>
                                        <div class="h-16 glass rounded border border-white/5"></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-20 relative">
        <div class="max-w-4xl mx-auto px-6 text-center">
            <div class="glass-strong rounded-3xl p-12 border border-white/10 reveal">
                <h2 class="font-display text-4xl font-bold mb-4">¿Tienes un <span class="text-gradient">proyecto</span>?</h2>
                <p class="text-gray-400 mb-8 text-lg">
                    Disponible para oportunidades remotas, reubicación o proyectos freelance.
                    <br>Construyamos algo extraordinario juntos.
                </p>
                
                <div class="flex flex-col sm:flex-row gap-4 justify-center mb-12">
                    <a href="mailto:sebayepa219@gmail.com" 
                       class="px-8 py-4 rounded-full bg-primary text-black font-semibold hover:shadow-[0_0_30px_rgba(0,217,255,0.4)] transition-all flex items-center justify-center gap-2">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
                        sebayepa219@gmail.com
                    </a>
                    <a href="https://linkedin.com/in/sebastianyepes-dev" target="_blank"
                       class="px-8 py-4 rounded-full glass border border-white/20 hover:border-primary/50 transition-all flex items-center justify-center gap-2">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
                        LinkedIn
                    </a>
                </div>

                <div class="flex justify-center gap-8 text-sm text-gray-500">
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></div>
                        Español Nativo
                    </div>
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-blue-500"></div>
                        Inglés B1 Profesional
                    </div>
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 rounded-full bg-purple-500"></div>
                        GMT-5 Colombia
                    </div>
                </div>
            </div>
            
            <div class="mt-12 text-gray-600 text-sm">
                <p>© 2025 Sebastian Yepes Padilla. Construido con precisión desde Medellín 🇨🇴</p>
            </div>
        </div>
    </section>

    <script>
        // Typewriter Effect
        const phrases = [
            "Optimizando bases de datos...",
            "Construyendo APIs escalables...",
            "Arquitectura Clean...",
            "Full Stack Developer"
        ];
        let phraseIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const typewriterElement = document.getElementById('typewriter-text');

        function typeWriter() {
            const currentPhrase = phrases[phraseIndex];
            
            if (isDeleting) {
                typewriterElement.textContent = currentPhrase.substring(0, charIndex - 1);
                charIndex--;
            } else {
                typewriterElement.textContent = currentPhrase.substring(0, charIndex + 1);
                charIndex++;
            }

            let typeSpeed = isDeleting ? 50 : 100;

            if (!isDeleting && charIndex === currentPhrase.length) {
                typeSpeed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                phraseIndex = (phraseIndex + 1) % phrases.length;
                typeSpeed = 500;
            }

            setTimeout(typeWriter, typeSpeed);
        }

        // Intersection Observer for reveal animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: "0px 0px -50px 0px"
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.reveal').forEach((el) => observer.observe(el));

        // Three.js Background Animation
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        document.getElementById('canvas-container').appendChild(renderer.domElement);

        // Create particles
        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 100;
        const posArray = new Float32Array(particlesCount * 3);

        for(let i = 0; i < particlesCount * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 5;
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        
        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.005,
            color: 0x00D9FF,
            transparent: true,
            opacity: 0.8,
        });

        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        camera.position.z = 3;

        // Mouse movement effect
        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener('mousemove', (event) => {
            mouseX = event.clientX / window.innerWidth - 0.5;
            mouseY = event.clientY / window.innerHeight - 0.5;
        });

        // Animation loop
        function animate() {
            requestAnimationFrame(animate);

            particlesMesh.rotation.y += 0.001;
            particlesMesh.rotation.x += 0.001;
            
            particlesMesh.rotation.x += mouseY * 0.05;
            particlesMesh.rotation.y += mouseX * 0.05;

            renderer.render(scene, camera);
        }

        animate();

        // Handle resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // Initialize typewriter
        setTimeout(typeWriter, 1000);
    </script>
</body>
</html>
