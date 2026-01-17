import React, { useState, useEffect } from 'react';
import { initializeApp } from 'firebase/app';
import { 
  getFirestore, 
  collection, 
  addDoc, 
  onSnapshot, 
  serverTimestamp,
  doc,
  deleteDoc,
  setDoc,
  query,
  updateDoc
} from 'firebase/firestore';
import { 
  getAuth, 
  signInAnonymously, 
  onAuthStateChanged,
  signInWithCustomToken 
} from 'firebase/auth';
import { 
  Trash2, 
  MapPin, 
  Phone, 
  User, 
  CheckCircle2,
  Package,
  Lock,
  Plus,
  Truck,
  PlusCircle,
  BarChart3,
  Loader2,
  Settings,
  X,
  Image as ImageIcon,
  Coins,
  ArrowRight,
  Leaf,
  Tag,
  TrendingUp
} from 'lucide-react';

const ADMIN_PASSWORD = "1234"; 
const TARGET_AMOUNT = 50; 

const firebaseConfig = JSON.parse(__firebase_config);
const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'recycle-premium-v5';

const App = () => {
  const [user, setUser] = useState(null);
  const [activeTab, setActiveTab] = useState('home'); 
  const [password, setPassword] = useState('');
  const [reports, setReports] = useState([]);
  const [wasteTypes, setWasteTypes] = useState([]);
  const [tambons, setTambons] = useState([]);
  const [loading, setLoading] = useState(false);
  const [submitted, setSubmitted] = useState(false);

  const [formData, setFormData] = useState({ tambon: '', name: '', phone: '', address: '' });
  const [wasteValues, setWasteValues] = useState({});

  const [newTambon, setNewTambon] = useState('');
  const [newWaste, setNewWaste] = useState({ name: '', unit: '', image: '', price: '' });

  useEffect(() => {
    const initAuth = async () => {
      if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
        await signInWithCustomToken(auth, __initial_auth_token);
      } else {
        await signInAnonymously(auth);
      }
    };
    initAuth();
    onAuthStateChanged(auth, setUser);
  }, []);

  useEffect(() => {
    if (!user) return;
    
    const qReports = query(collection(db, 'artifacts', appId, 'public', 'data', 'waste_reports'));
    const unsubReports = onSnapshot(qReports, (snapshot) => {
      setReports(snapshot.docs.map(d => ({ id: d.id, ...d.data() })));
    });

    const qWaste = query(collection(db, 'artifacts', appId, 'public', 'data', 'waste_settings'));
    const unsubWaste = onSnapshot(qWaste, (snapshot) => {
      const data = snapshot.docs.map(d => ({ id: d.id, ...d.data() }));
      if (data.length === 0) {
        const defaults = [
          { id: '1', name: 'ขวดพลาสติกใส (PET)', unit: 'กิโลกรัม', price: '8', image: 'https://images.unsplash.com/photo-1591193512858-12ee2a13827d?auto=format&fit=crop&q=80&w=200' },
          { id: '2', name: 'ขวดแก้ว/เบียร์', unit: 'ลัง', price: '12', image: 'https://images.unsplash.com/photo-1536939459926-301728717817?auto=format&fit=crop&q=80&w=200' },
          { id: '3', name: 'กระป๋องอลูมิเนียม', unit: 'กิโลกรัม', price: '35', image: 'https://images.unsplash.com/photo-1536627242417-20ed13244252?auto=format&fit=crop&q=80&w=200' }
        ];
        defaults.forEach(item => setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'waste_settings', item.id), item));
      }
      setWasteTypes(data);
    });

    const qTambon = query(collection(db, 'artifacts', appId, 'public', 'data', 'tambon_settings'));
    const unsubTambon = onSnapshot(qTambon, (snapshot) => {
      const data = snapshot.docs.map(d => ({ id: d.id, ...d.data() }));
      if (data.length === 0) {
        const defaults = ['นาโป่ง', 'เมืองนา', 'หนองบัว'].map(name => ({ id: name, name }));
        defaults.forEach(item => setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'tambon_settings', item.id), item));
      }
      setTambons(data);
    });

    return () => { unsubReports(); unsubWaste(); unsubTambon(); };
  }, [user]);

  const handleSubmit = async (e) => {
    e.preventDefault();
    setLoading(true);
    try {
      await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'waste_reports'), {
        ...formData,
        waste: wasteValues,
        createdAt: serverTimestamp(),
      });
      setSubmitted(true);
    } catch (e) { console.error(e); } finally { setLoading(false); }
  };

  const addTambon = async () => {
    if (!newTambon) return;
    await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'tambon_settings', newTambon), { name: newTambon });
    setNewTambon('');
  };

  const removeTambon = async (id) => {
    await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'tambon_settings', id));
  };

  const addWasteType = async () => {
    if (!newWaste.name) return;
    const id = Date.now().toString();
    await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'waste_settings', id), newWaste);
    setNewWaste({ name: '', unit: '', image: '', price: '' });
  };

  const updatePrice = async (id, newPrice) => {
    await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'waste_settings', id), { price: newPrice });
  };

  const removeWasteType = async (id) => {
    await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'waste_settings', id));
  };

  const getTambonSummary = (name) => {
    const tReports = reports.filter(r => r.tambon === name);
    const total = tReports.reduce((sum, r) => {
      let rSum = 0;
      Object.values(r.waste || {}).forEach(v => rSum += (Number(v) || 0));
      return sum + rSum;
    }, 0);
    return { total, progress: Math.min(100, (total / TARGET_AMOUNT) * 100) };
  };

  if (submitted) return (
    <div className="min-h-screen bg-white flex items-center justify-center p-8 animate-in fade-in zoom-in duration-500">
      <div className="text-center max-w-sm w-full">
        <div className="w-24 h-24 bg-green-500 rounded-full flex items-center justify-center mx-auto mb-8 shadow-2xl shadow-green-100 text-white">
          <CheckCircle2 size={48} strokeWidth={3} />
        </div>
        <h2 className="text-3xl font-black mb-4">ส่งข้อมูลสำเร็จ!</h2>
        <p className="text-slate-400 mb-10 text-lg font-medium leading-relaxed">ข้อมูลของคุณถูกส่งเข้าระบบแล้ว <br/>เตรียมรับเงินและช่วยโลกไปพร้อมกัน</p>
        <button onClick={() => { setSubmitted(false); setActiveTab('status'); }} className="w-full py-5 bg-slate-900 text-white rounded-[2.5rem] font-black shadow-xl hover:bg-slate-800 transition-all">ตรวจสอบสถานะ</button>
      </div>
    </div>
  );

  return (
    <div className="min-h-screen bg-[#FDFDFD] text-slate-900 pb-36 font-sans">
      <header className="px-6 py-6 bg-white/70 backdrop-blur-xl border-b border-slate-50 flex justify-between items-center sticky top-0 z-40">
        <div className="flex items-center gap-3">
          <div className="w-12 h-12 bg-gradient-to-tr from-green-400 to-emerald-600 rounded-2xl flex items-center justify-center text-white shadow-lg shadow-green-200">
            <Trash2 size={24} strokeWidth={2.5} />
          </div>
          <div>
            <h1 className="font-black text-2xl tracking-tighter leading-none uppercase">Recycle<span className="text-green-500">Pro</span></h1>
            <p className="text-[10px] text-slate-400 font-black uppercase tracking-[0.2em] mt-1">Smarter Earth, Better Life</p>
          </div>
        </div>
        {!user && <Loader2 size={20} className="animate-spin text-slate-300" />}
      </header>

      <main className="max-w-xl mx-auto p-6 pt-10">
        
        {activeTab === 'home' && (
          <div className="space-y-10 animate-in fade-in slide-in-from-bottom-6 duration-500">
            <div className="space-y-4">
              <div className="inline-flex items-center gap-2 px-3 py-1 bg-green-50 text-green-600 rounded-full text-[10px] font-black uppercase tracking-wider">
                <Coins size={12} /> Earn more from recycling
              </div>
              <h2 className="text-4xl sm:text-5xl font-black tracking-tight leading-[1.2] text-slate-900">
                เปลี่ยนขยะ <br/>
                <span className="text-green-500 text-3xl sm:text-4xl block mt-1">ให้เป็นขุมทรัพย์</span>
              </h2>
              
              {/* ตารางราคารับซื้อ (Show Prices) */}
              <div className="bg-white/50 border border-slate-100 rounded-3xl p-4 flex gap-4 overflow-x-auto no-scrollbar py-6 mt-4">
                {wasteTypes.map(w => (
                  <div key={w.id} className="min-w-[140px] bg-white p-4 rounded-2xl shadow-sm border border-slate-50 shrink-0">
                    <div className="flex items-center gap-2 text-[10px] font-black text-green-500 uppercase tracking-widest mb-1">
                      <TrendingUp size={10} /> ราคาดี
                    </div>
                    <span className="text-xs font-bold text-slate-400 block truncate">{w.name}</span>
                    <div className="flex items-baseline gap-1 mt-2">
                      <span className="text-xl font-black text-slate-900">฿{w.price || 0}</span>
                      <span className="text-[10px] font-bold text-slate-300">/{w.unit}</span>
                    </div>
                  </div>
                ))}
              </div>
            </div>

            <form onSubmit={handleSubmit} className="space-y-8">
              {/* พื้นที่บริการ */}
              <section className="bg-white p-8 rounded-[3rem] shadow-sm border border-slate-50">
                <div className="flex items-center gap-3 mb-6">
                   <div className="w-8 h-8 bg-slate-50 rounded-xl flex items-center justify-center text-slate-400"><MapPin size={18}/></div>
                   <h3 className="text-sm font-black uppercase tracking-widest text-slate-400">เลือกพื้นที่บริการ</h3>
                </div>
                <div className="grid grid-cols-2 gap-3">
                  {tambons.map(t => (
                    <button key={t.id} type="button" onClick={() => setFormData({...formData, tambon: t.name})} className={`py-4 rounded-2xl font-black text-sm border-2 transition-all ${formData.tambon === t.name ? 'bg-slate-900 border-slate-900 text-white shadow-2xl scale-105' : 'bg-white border-slate-50 text-slate-300 hover:border-slate-100'}`}>
                      {t.name}
                    </button>
                  ))}
                </div>
              </section>

              {/* รายการขยะ */}
              <section className="bg-white p-8 rounded-[3rem] shadow-sm border border-slate-50">
                <div className="flex items-center gap-3 mb-6">
                   <div className="w-8 h-8 bg-slate-50 rounded-xl flex items-center justify-center text-slate-400"><Package size={18}/></div>
                   <h3 className="text-sm font-black uppercase tracking-widest text-slate-400">ระบุรายการขยะ</h3>
                </div>
                <div className="space-y-4">
                  {wasteTypes.map(w => (
                    <div key={w.id} className="flex items-center gap-4 p-4 rounded-3xl bg-slate-50/30 border border-slate-50 hover:bg-white hover:border-green-100 hover:shadow-xl hover:shadow-green-50/50 transition-all group">
                      <div className="w-20 h-20 rounded-2xl overflow-hidden bg-white shrink-0 shadow-md group-hover:scale-105 transition-transform duration-500 border border-slate-100">
                        {w.image ? (
                          <img src={w.image} alt={w.name} className="w-full h-full object-cover" />
                        ) : (
                          <div className="w-full h-full flex items-center justify-center text-slate-200"><ImageIcon size={28}/></div>
                        )}
                      </div>
                      <div className="flex-1 min-w-0">
                        <span className="text-base font-black text-slate-800 block truncate leading-tight">{w.name}</span>
                        <div className="flex items-center gap-2 mt-1">
                          <span className="text-[10px] text-green-500 font-black">฿{w.price}/{w.unit}</span>
                        </div>
                      </div>
                      <div className="bg-white rounded-2xl p-1 shadow-inner border border-slate-100">
                        <input type="number" min="0" placeholder="0" className="w-14 p-2 bg-transparent text-center font-black text-lg outline-none" onChange={(e) => setWasteValues({...wasteValues, [w.id]: parseInt(e.target.value) || 0})} />
                      </div>
                    </div>
                  ))}
                </div>
              </section>

              {/* ข้อมูลติดต่อ */}
              <section className="bg-slate-900 p-10 rounded-[4rem] text-white space-y-5 shadow-2xl relative overflow-hidden">
                <div className="absolute top-0 right-0 p-8 opacity-10 rotate-12"><Truck size={120} /></div>
                <div className="relative z-10 flex items-center gap-3 mb-4">
                   <div className="w-8 h-8 bg-white/10 rounded-xl flex items-center justify-center text-white/40"><User size={18}/></div>
                   <h3 className="text-sm font-black uppercase tracking-widest text-white/40">ข้อมูลจุดรับขยะ</h3>
                </div>
                <div className="relative z-10 space-y-4">
                  <input required placeholder="ชื่อ-นามสกุล ของคุณ" className="w-full bg-white/5 border border-white/10 p-5 rounded-2xl outline-none font-bold text-sm focus:bg-white/10 focus:border-white/30 placeholder:text-white/20" value={formData.name} onChange={(e) => setFormData({...formData, name: e.target.value})} />
                  <input required type="tel" placeholder="เบอร์โทรศัพท์ติดต่อ" className="w-full bg-white/5 border border-white/10 p-5 rounded-2xl outline-none font-bold text-sm focus:bg-white/10 focus:border-white/30 placeholder:text-white/20" value={formData.phone} onChange={(e) => setFormData({...formData, phone: e.target.value})} />
                  <textarea required placeholder="บ้านเลขที่ หรือ จุดสังเกต" rows="2" className="w-full bg-white/5 border border-white/10 p-5 rounded-2xl outline-none font-bold text-sm focus:bg-white/10 focus:border-white/30 placeholder:text-white/20" value={formData.address} onChange={(e) => setFormData({...formData, address: e.target.value})} />
                </div>
              </section>

              <button type="submit" disabled={!formData.tambon || loading} className="w-full py-6 bg-green-500 text-slate-900 rounded-[2.5rem] font-black text-xl shadow-2xl shadow-green-200 active:scale-95 transition-all flex items-center justify-center gap-3 group">
                {loading ? <Loader2 className="animate-spin" /> : <>เรียกรถรับขยะตอนนี้ <ArrowRight className="group-hover:translate-x-2 transition-transform" /></>}
              </button>
            </form>
          </div>
        )}

        {/* หน้าสถานะ */}
        {activeTab === 'status' && (
          <div className="space-y-8 animate-in fade-in">
            <div className="space-y-2">
              <h2 className="text-4xl font-black tracking-tight">Status <span className="text-slate-300">Live</span></h2>
            </div>
            <div className="grid gap-6">
              {tambons.map(t => {
                const { total, progress } = getTambonSummary(t.name);
                const isReady = total >= TARGET_AMOUNT;
                return (
                  <div key={t.id} className="bg-white p-8 rounded-[3rem] border border-slate-50 shadow-sm relative overflow-hidden group">
                    <div className="flex justify-between items-center mb-6 relative z-10">
                      <div><h3 className="text-2xl font-black text-slate-900">ต.{t.name}</h3></div>
                      <div className={`px-4 py-2 rounded-2xl text-[10px] font-black flex items-center gap-2 shadow-lg ${isReady ? 'bg-green-500 text-white shadow-green-100' : 'bg-slate-100 text-slate-400 shadow-slate-50'}`}>
                        {isReady ? "พร้อมออกรอบ" : "กำลังรวบรวม"}
                      </div>
                    </div>
                    <div className="h-4 bg-slate-50 rounded-full overflow-hidden mb-4 p-1 border border-slate-50 relative z-10">
                      <div className={`h-full rounded-full transition-all duration-1000 ${isReady ? 'bg-gradient-to-r from-green-400 to-green-600' : 'bg-slate-300'}`} style={{ width: `${progress}%` }}></div>
                    </div>
                  </div>
                );
              })}
            </div>
          </div>
        )}

        {/* แอดมิน: ล็อกอิน */}
        {activeTab === 'admin-login' && (
          <div className="pt-24 animate-in zoom-in-95">
            <div className="bg-white p-12 rounded-[4rem] shadow-2xl text-center border border-slate-50">
              <div className="w-20 h-20 bg-slate-50 rounded-3xl flex items-center justify-center mx-auto mb-8 text-slate-900 shadow-inner"><Lock size={36}/></div>
              <h2 className="text-2xl font-black mb-8">Staff Authentication</h2>
              <input type="password" placeholder="Passcode" className="w-full p-5 bg-slate-50 rounded-2xl text-center font-black mb-6 outline-none border-2 border-transparent focus:border-slate-900 text-3xl tracking-[0.4em]" value={password} onChange={(e) => setPassword(e.target.value)} />
              <button onClick={() => password === ADMIN_PASSWORD ? setActiveTab('admin-panel') : alert('รหัสผ่านไม่ถูกต้อง')} className="w-full py-5 bg-slate-900 text-white rounded-2xl font-black shadow-xl transition-all">Unlock Dashboard</button>
            </div>
          </div>
        )}

        {/* แอดมิน: จัดการข้อมูล */}
        {activeTab === 'admin-panel' && (
          <div className="space-y-10 animate-in fade-in pb-20">
            <div className="flex justify-between items-center px-2">
              <h2 className="text-3xl font-black tracking-tight italic uppercase text-slate-900">Control<span className="text-green-500">Center</span></h2>
              <button onClick={() => {setActiveTab('admin-login'); setPassword('');}} className="text-[10px] font-black text-slate-400 uppercase bg-white px-4 py-2 rounded-xl border border-slate-100 shadow-sm">Logout</button>
            </div>

            {/* ส่วนจัดการขยะและราคา */}
            <section className="bg-white p-8 rounded-[3.5rem] shadow-sm border border-slate-100">
              <div className="flex items-center gap-2 mb-8 font-black text-slate-400 text-xs uppercase tracking-[0.3em]">
                <Tag size={16}/> จัดการราคารับซื้อ
              </div>
              <div className="grid gap-4 mb-8">
                {wasteTypes.map(w => (
                  <div key={w.id} className="p-5 bg-slate-50/50 rounded-3xl border border-slate-50">
                    <div className="flex items-center justify-between mb-4">
                       <div className="flex items-center gap-3">
                          <img src={w.image} className="w-10 h-10 rounded-xl object-cover" alt="" />
                          <span className="text-sm font-black text-slate-800">{w.name}</span>
                       </div>
                       <button onClick={() => removeWasteType(w.id)} className="text-slate-300 hover:text-red-500"><X size={16}/></button>
                    </div>
                    <div className="flex items-center gap-3 bg-white p-1 rounded-2xl shadow-inner border border-slate-100">
                      <div className="flex-1 flex items-center px-4 font-black text-xs text-slate-400">ราคาล่าสุด: ฿</div>
                      <input 
                        type="number" 
                        defaultValue={w.price} 
                        className="w-24 p-3 bg-slate-50 rounded-xl font-black text-right outline-none" 
                        onBlur={(e) => updatePrice(w.id, e.target.value)}
                        placeholder="0"
                      />
                      <div className="px-4 text-[10px] font-black text-slate-300 uppercase">/{w.unit}</div>
                    </div>
                  </div>
                ))}
              </div>
              
              <div className="space-y-3 pt-6 border-t border-slate-50">
                <div className="grid grid-cols-2 gap-2">
                  <input placeholder="ชื่อขยะ" className="p-4 bg-slate-50 rounded-2xl text-sm font-bold outline-none" value={newWaste.name} onChange={e => setNewWaste({...newWaste, name: e.target.value})} />
                  <input placeholder="หน่วย (กก./ลัง)" className="p-4 bg-slate-50 rounded-2xl text-sm font-bold outline-none" value={newWaste.unit} onChange={e => setNewWaste({...newWaste, unit: e.target.value})} />
                </div>
                <input placeholder="ราคาเริ่มต้น (บาท)" type="number" className="w-full p-4 bg-slate-50 rounded-2xl text-sm font-bold outline-none" value={newWaste.price} onChange={e => setNewWaste({...newWaste, price: e.target.value})} />
                <input placeholder="ลิงก์รูปภาพ (URL)" className="w-full p-4 bg-slate-50 rounded-2xl text-sm font-bold outline-none" value={newWaste.image} onChange={e => setNewWaste({...newWaste, image: e.target.value})} />
                <button onClick={addWasteType} className="w-full py-4 bg-green-500 text-white rounded-2xl font-black flex items-center justify-center gap-2"><Plus size={18}/> เพิ่มรายการใหม่</button>
              </div>
            </section>

            {/* จัดการตำบล */}
            <section className="bg-white p-8 rounded-[3.5rem] shadow-sm border border-slate-100">
              <div className="flex items-center gap-2 mb-8 font-black text-slate-400 text-xs uppercase tracking-[0.3em]"><MapPin size={16}/> พื้นที่บริการ</div>
              <div className="flex flex-wrap gap-2 mb-6">
                {tambons.map(t => (
                  <div key={t.id} className="bg-slate-900 text-white px-5 py-2.5 rounded-2xl text-xs font-black flex items-center gap-3">
                    {t.name} <button onClick={() => removeTambon(t.id)}><X size={14}/></button>
                  </div>
                ))}
              </div>
              <div className="flex gap-2">
                <input placeholder="ชื่อตำบลใหม่" className="flex-1 p-4 bg-slate-50 rounded-2xl text-sm font-bold outline-none" value={newTambon} onChange={e => setNewTambon(e.target.value)} />
                <button onClick={addTambon} className="w-14 h-14 bg-slate-900 text-white rounded-2xl flex items-center justify-center"><Plus size={24}/></button>
              </div>
            </section>

            {/* รายงานการแจ้งรับ */}
            <section className="space-y-4">
              <label className="text-[10px] font-black text-slate-400 uppercase px-4">Pending Tasks ({reports.length})</label>
              {reports.map(r => (
                <div key={r.id} className="bg-white p-8 rounded-[3.5rem] border border-slate-100 shadow-sm group">
                   <div className="flex justify-between items-start mb-6">
                      <div className="flex gap-4">
                        <div className="w-12 h-12 bg-green-50 rounded-2xl flex items-center justify-center text-green-600"><User size={24}/></div>
                        <div>
                          <h4 className="font-black text-xl text-slate-900">{r.name}</h4>
                          <span className="text-[10px] font-black text-slate-400 uppercase tracking-widest mt-1 block">ต.{r.tambon} • {r.phone}</span>
                        </div>
                      </div>
                      <button onClick={async () => {if(window.confirm('เสร็จงานแล้ว?')) await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'waste_reports', r.id))}} className="w-12 h-12 bg-red-50 text-red-500 rounded-2xl flex items-center justify-center"><Trash2 size={20}/></button>
                   </div>
                   <div className="bg-slate-50 p-6 rounded-3xl mb-4 text-xs font-bold text-slate-500 leading-relaxed italic">{r.address}</div>
                   <div className="flex gap-2 flex-wrap">
                      {Object.entries(r.waste || {}).filter(([_, v]) => v > 0).map(([kid, val]) => {
                        const w = wasteTypes.find(x => x.id === kid);
                        return (
                          <div key={kid} className="bg-slate-900 text-white px-4 py-2 rounded-xl text-[10px] font-black">
                            {w?.name}: <span className="text-green-400">{val} {w?.unit}</span>
                          </div>
                        );
                      })}
                   </div>
                </div>
              ))}
            </section>
          </div>
        )}
      </main>

      {/* Navigation */}
      <nav className="fixed bottom-8 left-1/2 -translate-x-1/2 w-[85%] max-w-sm h-22 bg-slate-900/95 backdrop-blur-3xl rounded-[3rem] flex justify-around items-center z-50 shadow-2xl border border-white/10 px-6 py-2">
        <button onClick={() => setActiveTab('home')} className={`group flex flex-col items-center gap-1.5 transition-all ${activeTab === 'home' ? 'text-green-400' : 'text-slate-500'}`}>
          <div className={`p-2 rounded-2xl ${activeTab === 'home' ? 'bg-green-400/10' : ''}`}><PlusCircle size={24} strokeWidth={activeTab === 'home' ? 3 : 2}/></div>
          <span className="text-[8px] font-black uppercase tracking-[0.2em]">แจ้งรับ</span>
        </button>
        <button onClick={() => setActiveTab('status')} className={`group flex flex-col items-center gap-1.5 transition-all ${activeTab === 'status' ? 'text-green-400' : 'text-slate-500'}`}>
          <div className={`p-2 rounded-2xl ${activeTab === 'status' ? 'bg-green-400/10' : ''}`}><BarChart3 size={24} strokeWidth={activeTab === 'status' ? 3 : 2}/></div>
          <span className="text-[8px] font-black uppercase tracking-[0.2em]">สถานะ</span>
        </button>
        <button onClick={() => { if (activeTab !== 'admin-panel') setActiveTab('admin-login'); else setActiveTab('admin-panel'); }} className={`group flex flex-col items-center gap-1.5 transition-all ${activeTab.includes('admin') ? 'text-green-400' : 'text-slate-500'}`}>
          <div className={`p-2 rounded-2xl ${activeTab.includes('admin') ? 'bg-green-400/10' : ''}`}><Settings size={24} strokeWidth={activeTab.includes('admin') ? 3 : 2}/></div>
          <span className="text-[8px] font-black uppercase tracking-[0.2em]">แอดมิน</span>
        </button>
      </nav>
    </div>
  );
};

export default App;
