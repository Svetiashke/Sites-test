
import React, { useRef, useState, useEffect, Suspense } from "react"; import { Canvas, useFrame, useThree } from "@react-three/fiber"; import { Text, Stars, OrbitControls } from "@react-three/drei"; import { motion } from "framer-motion";

// Helper: simple particles cloud function Particles({ count = 300 }) { const mesh = useRef(); const positions = useRef();

if (!positions.current) { positions.current = new Float32Array(count * 3); for (let i = 0; i < count; i++) { const i3 = i * 3; positions.current[i3 + 0] = (Math.random() - 0.5) * 40; positions.current[i3 + 1] = (Math.random() - 0.5) * 20; positions.current[i3 + 2] = (Math.random() - 0.5) * 40; } }

useFrame((state) => { if (!mesh.current) return; mesh.current.rotation.y += 0.0005; const time = state.clock.getElapsedTime(); for (let i = 0; i < count; i++) { const i3 = i * 3 + 1; positions.current[i3] += Math.sin(time + i) * 0.0005; } mesh.current.geometry.attributes.position.needsUpdate = true; });

return ( <points ref={mesh}> <bufferGeometry> <bufferAttribute attachObject={"attributes-position"} count={positions.current.length / 3} array={positions.current} itemSize={3} /> </bufferGeometry> <pointsMaterial size={0.08} sizeAttenuation={true} /> </points> ); }

// Floating headline text function FloatingText({ text = "Your Name" }) { const ref = useRef(); useFrame((state) => { const t = state.clock.getElapsedTime(); ref.current.position.y = Math.sin(t * 0.7) * 0.6 + 1.2; ref.current.rotation.y = Math.sin(t * 0.2) * 0.1; }); return ( <Text
ref={ref}
fontSize={0.9}
maxWidth={6}
lineHeight={1}
letterSpacing={-0.05}
anchorX="center"
anchorY="middle"
depthOffset={0.5}
castShadow
> {text} </Text> ); }

// Camera controller function CameraRig({ target = "home" }) { const { camera } = useThree(); const targets = { home: { x: 0, y: 1.8, z: 6 }, about: { x: 0, y: 1.5, z: 4 }, projects: { x: -6, y: 1.8, z: 5 }, contact: { x: 6, y: 1.8, z: 5 }, };

useFrame((state, delta) => { const dest = targets[target] || targets.home; camera.position.x += (dest.x - camera.position.x) * Math.min(delta * 3, 1); camera.position.y += (dest.y - camera.position.y) * Math.min(delta * 3, 1); camera.position.z += (dest.z - camera.position.z) * Math.min(delta * 3, 1); camera.lookAt(0, 1, 0); });

return null; }

// Main Portfolio Component export default function Portfolio3D() { const [section, setSection] = useState("home");

useEffect(() => { const handler = (e) => { if (e.key === "1") setSection("home"); if (e.key === "2") setSection("about"); if (e.key === "3") setSection("projects"); if (e.key === "4") setSection("contact"); }; window.addEventListener("keydown", handler); return () => window.removeEventListener("keydown", handler); }, []);

return ( <div className="w-screen h-screen bg-black text-white overflow-hidden relative"> <Canvas camera={{ position: [0, 1.8, 6], fov: 50 }} shadows> <ambientLight intensity={0.6} /> <directionalLight position={[5, 10, 5]} intensity={1} /> <Suspense fallback={null}> <Stars radius={100} depth={50} count={5000} factor={4} saturation={0} fade /> <Particles count={600} /> <FloatingText text={"Your Name"} /> <CameraRig target={section} /> </Suspense> <OrbitControls enablePan={false} enableZoom={false} enableRotate={false} /> </Canvas>

<div className="absolute inset-0 pointer-events-none">
    <div className="absolute left-6 top-6 pointer-events-auto">
      <nav className="flex flex-col gap-3">
        <button className={`px-3 py-1 rounded-md text-sm backdrop-blur-sm bg-white/5 hover:bg-white/10 transition-all ${section === "home" ? "ring-2 ring-white/30" : ""}`} onClick={() => setSection("home")}>Home</button>
        <button className={`px-3 py-1 rounded-md text-sm backdrop-blur-sm bg-white/5 hover:bg-white/10 transition-all ${section === "about" ? "ring-2 ring-white/30" : ""}`} onClick={() => setSection("about")}>About</button>
        <button className={`px-3 py-1 rounded-md text-sm backdrop-blur-sm bg-white/5 hover:bg-white/10 transition-all ${section === "projects" ? "ring-2 ring-white/30" : ""}`} onClick={() => setSection("projects")}>Projects</button>
        <button className={`px-3 py-1 rounded-md text-sm backdrop-blur-sm bg-white/5 hover:bg-white/10 transition-all ${section === "contact" ? "ring-2 ring-white/30" : ""}`} onClick={() => setSection("contact")}>Contact</button>
      </nav>
    </div>

    <div className="absolute inset-0 flex items-center justify-center pointer-events-auto">
      <motion.div key={section} initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -20 }} transition={{ duration: 0.6 }} className="max-w-3xl mx-6 p-8 rounded-2xl bg-gradient-to-br from-black/40 to-black/30 border border-white/5 backdrop-blur-md">
        {section === "home" && (
          <div>
            <h1 className="text-4xl font-bold">Привіт — я Your Name</h1>
            <p className="mt-3 text-lg text-white/80">Креативний дизайнер / 3D & web developer</p>
            <div className="mt-6 flex gap-3">
              <button className="px-4 py-2 rounded-md bg-white/10 backdrop-blur-sm">Дивитись роботи</button>
              <button className="px-4 py-2 rounded-md bg-white/6">Зв'язатись</button>
            </div>
          </div>
        )}
        {section === "about" && (
          <div>
            <h2 className="text-3xl font-semibold">Про мене</h2>
            <p className="mt-3 text-white/80 leading-relaxed">Коротко: я створюю інтерактивні веб-досвіди з 3D-графікою. Люблю гру з світлом, частинками та анімацією. Працюю з React, Three.js та творчим дизайном.</p>
          </div>
        )}
        {section === "projects" && (
          <div>
            <h2 className="text-3xl font-semibold">Проєкти</h2>
            <div className="mt-4 grid grid-cols-1 md:grid-cols-

