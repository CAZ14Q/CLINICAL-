import React, { useState, useEffect, useMemo } from 'react';
import { initializeApp } from 'firebase/app';
import { getAuth, signInAnonymously, onAuthStateChanged, signInWithCustomToken, signOut } from 'firebase/auth';
import { 
  getFirestore, collection, addDoc, onSnapshot, doc, 
  updateDoc, deleteDoc, serverTimestamp, query, orderBy 
} from 'firebase/firestore';
import { 
  Users, Plus, Search, Phone, Calendar, ClipboardList, 
  Edit3, X, AlertCircle, Clock, LayoutDashboard, 
  ChevronLeft, FileText, ArrowRight, Image as ImageIcon, 
  History, FileUp, ExternalLink, Activity, Database,
  Trash2, Download, LogOut, CheckCircle2, UserCircle
} from 'lucide-react';

// --- تهيئة Firebase ---
const firebaseConfig = JSON.parse(__firebase_config);
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'clinica-pro-stable-v1';

export default function App() {
  const [user, setUser] = useState(null);
  const [patients, setPatients] = useState([]);
  const [appointments, setAppointments] = useState([]);
  const [search, setSearch] = useState('');
  const [activeTab, setActiveTab] = useState('dashboard');
  const [selectedPatientId, setSelectedPatientId] = useState(null);
  
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [isApptModalOpen, setIsApptModalOpen] = useState(false);
  const [isEditMode, setIsEditMode] = useState(false);
  const [loading, setLoading] = useState(false);

  const [formData, setFormData] = useState({
    name: '', phone: '', condition: '', status: 'Active', 
    age: '', gender: 'Male', history: [], nextVisit: ''
  });

  const [apptData, setApptData] = useState({
    patientId: '', date: '', time: '', note: '', status: 'Pending'
  });

  // --- Auth ---
  useEffect(() => {
    const initAuth = async () => {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (e) { console.error("Auth Error", e); }
    };
    initAuth();
    return onAuthStateChanged(auth, setUser);
  }, []);

  // --- Real-time Data ---
  useEffect(() => {
    if (!user) return;

    const pRef = collection(db, 'artifacts', appId, 'users', user.uid, 'patients');
    const unsubPatients = onSnapshot(pRef, (snap) => {
      setPatients(snap.docs.map(d => ({ id: d.id, ...d.data() })));
    }, (err) => console.error("Firestore Error", err));

    const aRef = collection(db, 'artifacts', appId, 'users', user.uid, 'appointments');
    const unsubAppts = onSnapshot(aRef, (snap) => {
      setAppointments(snap.docs.map(d => ({ id: d.id, ...d.data() })));
    }, (err) => console.error("Firestore Error", err));

    return () => { unsubPatients(); unsubAppts(); };
  }, [user]);

  // --- Handlers ---
  const handleSavePatient = async (e) => {
    e.preventDefault();
    if (!user) return;
    setLoading(true);
    try {
      const pRef = collection(db, 'artifacts', appId, 'users', user.uid, 'patients');
      if (isEditMode && selectedPatientId) {
        await updateDoc(doc(pRef, selectedPatientId), { ...formData });
      } else {
        await addDoc(pRef, { ...formData, createdAt: serverTimestamp() });
      }
      setIsModalOpen(false);
      resetForm();
    } catch (err) { console.error(err); } finally { setLoading(false); }
  };

  const resetForm = () => {
    setFormData({ name: '', phone: '', condition: '', status: 'Active', age: '', gender: 'Male', history: [], nextVisit: '' });
    setIsEditMode(false);
  };

  const deletePatient = async (id) => {
    if (!user || !window.confirm("هل أنت متأكد من حذف هذا المريض نهائياً؟")) return;
    await deleteDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'patients', id));
  };

  const handleAddAppointment = async (e) => {
    e.preventDefault();
    if (!user) return;
    const p = patients.find(px => px.id === apptData.patientId);
    await addDoc(collection(db, 'artifacts', appId, 'users', user.uid, 'appointments'), {
      ...apptData,
      patientName: p ? p.name : 'Unknown',
      createdAt: serverTimestamp()
    });
    setIsApptModalOpen(false);
  };

  const printReport = (p) => {
    const printWindow = window.open('', '_blank');
    printWindow.document.write(`
      <div style="direction: rtl; font-family: sans-serif; padding: 40px;">
        <h1 style="color: #2563eb;">تقرير طبي: ${p.name}</h1>
        <hr/>
        <p><b>رقم الهاتف:</b> ${p.phone}</p>
        <p><b>العمر:</b> ${p.age}</p>
        <p><b>الحالة التشخيصية:</b> ${p.condition}</p>
        <p><b>حالة المريض:</b> ${p.status}</p>
        <h3>السجل الزمني:</h3>
        <ul>${(p.history || []).map(h => `<li>${h.date}: ${h.text}</li>`).join('')}</ul>
      </div>
    `);
    printWindow.document.close();
    printWindow.print();
  };

  const filtered = patients.filter(p => p.name?.includes(search) || p.phone?.includes(search));

  if (!user) return <div className="h-screen bg-[#070912] flex items-center justify-center text-blue-500 font-bold">جاري الاتصال بالسيرفر...</div>;

  return (
    <div className="min-h-screen bg-[#070912] text-slate-300 font-sans rtl flex" dir="rtl">
      
      {/* Sidebar */}
      <aside className="w-64 bg-[#0d111d] border-l border-white/5 flex flex-col shrink-0">
        <div className="p-8 flex-1">
          <div className="flex items-center gap-3 mb-12">
            <Activity size={28} className="text-blue-500"/>
            <h1 className="font-black text-xl text-white">Clinica<span className="text-blue-500">PRO</span></h1>
          </div>
          <nav className="space-y-2">
            <button onClick={() => setActiveTab('dashboard')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-xl transition ${activeTab === 'dashboard' ? 'bg-blue-600 text-white shadow-lg' : 'hover:bg-white/5'}`}>
              <LayoutDashboard size={18}/> <span className="text-sm font-bold">الرئيسية</span>
            </button>
            <button onClick={() => setActiveTab('records')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-xl transition ${activeTab === 'records' ? 'bg-blue-600 text-white shadow-lg' : 'hover:bg-white/5'}`}>
              <Users size={18}/> <span className="text-sm font-bold">المرضى</span>
            </button>
            <button onClick={() => setActiveTab('appointments')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-xl transition ${activeTab === 'appointments' ? 'bg-blue-600 text-white shadow-lg' : 'hover:bg-white/5'}`}>
              <Calendar size={18}/> <span className="text-sm font-bold">المواعيد</span>
            </button>
          </nav>
        </div>
        <div className="p-6 border-t border-white/5">
          <button onClick={() => signOut(auth)} className="flex items-center gap-3 text-slate-500 hover:text-red-500 w-full px-4"><LogOut size={16}/> خروج</button>
        </div>
      </aside>

      {/* Main Content */}
      <main className="flex-1 flex flex-col h-screen overflow-hidden">
        <header className="h-20 bg-[#070912] border-b border-white/5 px-8 flex items-center justify-between">
           <h2 className="text-white font-black text-lg">لوحة التحكم</h2>
           <div className="flex items-center gap-4">
              <div className="relative">
                <Search className="absolute right-3 top-1/2 -translate-y-1/2 text-slate-500" size={14}/>
                <input 
                  type="text" placeholder="بحث باسم المريض..." 
                  className="bg-white/5 border border-white/10 rounded-xl py-2 pr-10 pl-4 text-xs outline-none focus:border-blue-500 w-64"
                  value={search} onChange={e => setSearch(e.target.value)}
                />
              </div>
              <button onClick={() => {resetForm(); setIsModalOpen(true);}} className="bg-blue-600 hover:bg-blue-500 text-white px-5 py-2 rounded-xl font-bold text-xs flex items-center gap-2 shadow-lg shadow-blue-600/20">
                <Plus size={16}/> مريض جديد
              </button>
           </div>
        </header>

        <div className="flex-1 overflow-y-auto p-8 custom-scroll">
          
          {activeTab === 'dashboard' && (
            <div className="grid grid-cols-1 md:grid-cols-3 gap-6 animate-fade-in">
              <div className="bg-[#0d111d] p-6 rounded-3xl border border-white/5">
                <p className="text-[10px] font-black text-slate-500 uppercase mb-2">إجمالي المسجلين</p>
                <div className="text-3xl font-black text-white">{patients.length}</div>
              </div>
              <div className="bg-[#0d111d] p-6 rounded-3xl border border-white/5">
                <p className="text-[10px] font-black text-slate-500 uppercase mb-2">مواعيد قادمة</p>
                <div className="text-3xl font-black text-orange-500">{appointments.length}</div>
              </div>
              <div className="bg-[#0d111d] p-6 rounded-3xl border border-white/5">
                <p className="text-[10px] font-black text-slate-500 uppercase mb-2">حالات حرجة</p>
                <div className="text-3xl font-black text-red-500">{patients.filter(p => p.status === 'Critical').length}</div>
              </div>
            </div>
          )}

          {activeTab === 'records' && (
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 animate-fade-in">
              {filtered.map(p => (
                <div key={p.id} className="bg-[#0d111d] p-6 rounded-3xl border border-white/5 hover:border-blue-500/30 transition-all relative group">
                  <div className="flex justify-between items-start mb-4">
                    <div className="w-12 h-12 bg-blue-600/10 rounded-2xl flex items-center justify-center text-blue-500 font-black text-xl">{p.name?.[0]}</div>
                    <div className="flex gap-1 opacity-0 group-hover:opacity-100 transition-opacity">
                      <button onClick={() => {setFormData(p); setSelectedPatientId(p.id); setIsEditMode(true); setIsModalOpen(true);}} className="p-2 bg-white/5 rounded-lg hover:text-blue-500"><Edit3 size={14}/></button>
                      <button onClick={() => deletePatient(p.id)} className="p-2 bg-white/5 rounded-lg hover:text-red-500"><Trash2 size={14}/></button>
                    </div>
                  </div>
                  <h4 className="text-white font-bold">{p.name}</h4>
                  <p className="text-[10px] text-slate-500 mb-4">{p.phone}</p>
                  <div className="flex items-center justify-between border-t border-white/5 pt-4">
                    <span className={`text-[9px] font-black px-2 py-1 rounded-md ${p.status === 'Critical' ? 'bg-red-500/10 text-red-500' : 'bg-green-500/10 text-green-500'}`}>{p.status}</span>
                    <button onClick={() => printReport(p)} className="text-slate-500 hover:text-white transition"><Download size={14}/></button>
                  </div>
                </div>
              ))}
            </div>
          )}

          {activeTab === 'appointments' && (
            <div className="bg-[#0d111d] rounded-3xl border border-white/5 p-8 animate-fade-in">
               <div className="flex justify-between items-center mb-8">
                  <h3 className="text-white font-bold">جدول المواعيد</h3>
                  <button onClick={() => setIsApptModalOpen(true)} className="text-xs text-blue-500 font-bold hover:underline">+ حجز موعد جديد</button>
               </div>
               <div className="space-y-4">
                  {appointments.map(a => (
                    <div key={a.id} className="flex items-center justify-between p-4 bg-white/5 rounded-2xl border border-white/5">
                       <div className="flex items-center gap-4">
                          <div className="p-2 bg-blue-600/10 rounded-lg text-blue-500"><Clock size={16}/></div>
                          <div>
                             <p className="text-sm font-bold text-white">{a.patientName}</p>
                             <p className="text-[10px] text-slate-500">{a.date} - {a.time}</p>
                          </div>
                       </div>
                       <span className="text-[10px] font-black uppercase text-orange-500">{a.status}</span>
                    </div>
                  ))}
               </div>
            </div>
          )}

        </div>
      </main>

      {/* Modal - Patient */}
      {isModalOpen && (
        <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4">
          <div className="bg-[#0d111d] w-full max-w-lg rounded-[2rem] p-8 border border-white/10 relative">
            <button onClick={() => setIsModalOpen(false)} className="absolute top-6 left-6 text-slate-500 hover:text-white"><X/></button>
            <h3 className="text-xl font-black text-white mb-8">{isEditMode ? 'تعديل السجل' : 'مريض جديد'}</h3>
            <form onSubmit={handleSavePatient} className="space-y-4">
              <input placeholder="الاسم الكامل" required className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none focus:border-blue-500" value={formData.name} onChange={e => setFormData({...formData, name: e.target.value})} />
              <div className="grid grid-cols-2 gap-4">
                <input placeholder="رقم الهاتف" className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none focus:border-blue-500" value={formData.phone} onChange={e => setFormData({...formData, phone: e.target.value})} />
                <input placeholder="العمر" type="number" className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none focus:border-blue-500" value={formData.age} onChange={e => setFormData({...formData, age: e.target.value})} />
              </div>
              <textarea placeholder="التشخيص المبدئي" className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none focus:border-blue-500" value={formData.condition} onChange={e => setFormData({...formData, condition: e.target.value})} />
              <select className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none" value={formData.status} onChange={e => setFormData({...formData, status: e.target.value})}>
                <option value="Active">نشط</option>
                <option value="Critical">حرج</option>
                <option value="Recovered">متعافي</option>
              </select>
              <button type="submit" disabled={loading} className="w-full bg-blue-600 py-4 rounded-xl text-white font-black shadow-lg shadow-blue-600/20">{loading ? 'جاري الحفظ...' : 'حفظ البيانات'}</button>
            </form>
          </div>
        </div>
      )}

      {/* Modal - Appointment */}
      {isApptModalOpen && (
        <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4">
          <div className="bg-[#0d111d] w-full max-w-md rounded-[2rem] p-8 border border-white/10 relative">
             <button onClick={() => setIsApptModalOpen(false)} className="absolute top-6 left-6 text-slate-500 hover:text-white"><X/></button>
             <h3 className="text-xl font-black text-white mb-6">حجز موعد جديد</h3>
             <form onSubmit={handleAddAppointment} className="space-y-4">
                <select required className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none" onChange={e => setApptData({...apptData, patientId: e.target.value})}>
                   <option value="">اختر مريضاً</option>
                   {patients.map(p => <option key={p.id} value={p.id}>{p.name}</option>)}
                </select>
                <div className="grid grid-cols-2 gap-4">
                   <input type="date" required className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none" value={apptData.date} onChange={e => setApptData({...apptData, date: e.target.value})} />
                   <input type="time" required className="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm text-white outline-none" value={apptData.time} onChange={e => setApptData({...apptData, time: e.target.value})} />
                </div>
                <button type="submit" className="w-full bg-blue-600 py-4 rounded-xl text-white font-black shadow-lg shadow-blue-600/20">تأكيد الموعد</button>
             </form>
          </div>
        </div>
      )}

      <style dangerouslySetInnerHTML={{ __html: `
        .custom-scroll::-webkit-scrollbar { width: 4px; }
        .custom-scroll::-webkit-scrollbar-thumb { background: #1e293b; border-radius: 10px; }
        .animate-fade-in { animation: fadeIn 0.3s ease-out forwards; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
        select option { background: #0d111d; color: white; }
      `}} />
    </div>
  );
}
ابي اطور سجلات فقط وشكل 
