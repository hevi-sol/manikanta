<!DOCTYPE html>

<html lang="en">

<head>

&nbsp;   <meta charset="UTF-8">

&nbsp;   <meta name="viewport" content="width=device-width, initial-scale=1.0">

&nbsp;   <title>Manikanta Fine Dining | Authentic Indian Cuisine</title>

&nbsp;   <!-- Tailwind CSS for styling -->

&nbsp;   <script src="https://cdn.tailwindcss.com"></script>

&nbsp;   <!-- React and ReactDOM -->

&nbsp;   <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>

&nbsp;   <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

&nbsp;   <!-- Babel for JSX parsing -->

&nbsp;   <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

&nbsp;   <!-- Lucide Icons -->

&nbsp;   <script src="https://unpkg.com/lucide@latest"></script>

&nbsp;   <style>

&nbsp;       @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400\&family=Inter:wght@300;400;600\&display=swap');

&nbsp;       

&nbsp;       body { font-family: 'Playfair Display', serif; }

&nbsp;       .font-sans { font-family: 'Inter', sans-serif; }



&nbsp;       @keyframes fade-in {

&nbsp;           from { opacity: 0; transform: translateY(20px); }

&nbsp;           to { opacity: 1; transform: translateY(0); }

&nbsp;       }

&nbsp;       .animate-fade-in { animation: fade-in 1.2s ease-out forwards; }

&nbsp;       html { scroll-behavior: smooth; }

&nbsp;       

&nbsp;       /\* Custom scrollbar for premium look \*/

&nbsp;       ::-webkit-scrollbar { width: 8px; }

&nbsp;       ::-webkit-scrollbar-track { background: #f1f1f1; }

&nbsp;       ::-webkit-scrollbar-thumb { background: #888; border-radius: 4px; }

&nbsp;       ::-webkit-scrollbar-thumb:hover { background: #d97706; }

&nbsp;   </style>

</head>

<body>

&nbsp;   <div id="root"></div>



&nbsp;   <script type="text/babel">

&nbsp;       const { useState, useEffect } = React;



&nbsp;       // Simple Icon Component for CDN version

&nbsp;       const Icon = ({ name, size = 20, className = "" }) => {

&nbsp;           useEffect(() => {

&nbsp;               if (window.lucide) {

&nbsp;                   window.lucide.createIcons();

&nbsp;               }

&nbsp;           }, \[name]);

&nbsp;           return <i data-lucide={name} style={{ width: size, height: size }} className={className}></i>;

&nbsp;       };



&nbsp;       const App = () => {

&nbsp;           const \[isMenuOpen, setIsMenuOpen] = useState(false);

&nbsp;           const \[activeCategory, setActiveCategory] = useState('All');

&nbsp;           const \[scrolled, setScrolled] = useState(false);

&nbsp;           const \[showStatus, setShowStatus] = useState(null);



&nbsp;           useEffect(() => {

&nbsp;               const handleScroll = () => setScrolled(window.scrollY > 50);

&nbsp;               window.addEventListener('scroll', handleScroll);

&nbsp;               

&nbsp;               const urlParams = new URLSearchParams(window.location.search);

&nbsp;               if (urlParams.get('status') === 'success') {

&nbsp;                   setShowStatus('success');

&nbsp;                   setTimeout(() => setShowStatus(null), 5000);

&nbsp;               } else if (urlParams.get('status') === 'error') {

&nbsp;                   setShowStatus('error');

&nbsp;                   setTimeout(() => setShowStatus(null), 5000);

&nbsp;               }



&nbsp;               return () => window.removeEventListener('scroll', handleScroll);

&nbsp;           }, \[]);



&nbsp;           const menuCategories = \['All', 'Starters', 'Main Course', 'Biryani', 'Desserts'];

&nbsp;           const menuItems = \[

&nbsp;               { id: 1, name: 'Paneer Butter Masala', category: 'Main Course', price: 199, rating: 4.8, description: 'Cubes of cottage cheese in a rich tomato-based gravy.' },

&nbsp;               { id: 2, name: 'Special Veg Biryani', category: 'Biryani', price: 199, rating: 4.9, description: 'Fragrant basmati rice cooked with fresh garden vegetables.' },

&nbsp;               { id: 3, name: 'Gobi Manchurian', category: 'Starters', price: 199, rating: 4.7, description: 'Crispy cauliflower florets tossed in spicy Manchurian sauce.' },

&nbsp;               { id: 4, name: 'Dal Makhani Gold', category: 'Main Course', price: 199, rating: 4.6, description: 'Black lentils slow-cooked overnight with cream and butter.' },

&nbsp;               { id: 5, name: 'Gulab Jamun with Ice Cream', category: 'Desserts', price: 199, rating: 4.9, description: 'Warm syrup-soaked dumplings served with vanilla bean ice cream.' },

&nbsp;               { id: 6, name: 'Paneer Tikka', category: 'Starters', price: 199, rating: 4.8, description: 'Clay oven roasted paneer marinated in royal spices.' },

&nbsp;           ];



&nbsp;           const filteredMenu = activeCategory === 'All' ? menuItems : menuItems.filter(item => item.category === activeCategory);



&nbsp;           const handleRazorpay = (itemName) => {

&nbsp;               // Mock Razorpay Implementation

&nbsp;               alert(`Opening Razorpay Gateway...\\nProduct: ${itemName}\\nAmount: ₹199`);

&nbsp;           };



&nbsp;           const openWhatsApp = () => {

&nbsp;               const message = encodeURIComponent("Hello Manikanta Fine Dining! I would like to book a table.");

&nbsp;               window.open(`https://wa.me/918341950743?text=${message}`, '\_blank');

&nbsp;           };



&nbsp;           return (

&nbsp;               <div className="min-h-screen bg-stone-50 text-stone-900 overflow-x-hidden">

&nbsp;                   {/\* Floating WhatsApp \*/}

&nbsp;                   <button onClick={openWhatsApp} className="fixed bottom-6 right-6 z-\[100] bg-green-500 text-white p-4 rounded-full shadow-2xl hover:scale-110 transition-transform flex items-center justify-center">

&nbsp;                       <Icon name="message-circle" size={28} />

&nbsp;                   </button>



&nbsp;                   {/\* Status Note \*/}

&nbsp;                   {showStatus \&\& (

&nbsp;                       <div className={`fixed top-24 right-6 z-\[100] p-4 flex items-center gap-3 shadow-xl animate-fade-in ${showStatus === 'success' ? 'bg-green-600' : 'bg-red-600'} text-white rounded-lg`}>

&nbsp;                           <Icon name={showStatus === 'success' ? "check-circle" : "x"} size={20} />

&nbsp;                           <span className="font-sans text-sm tracking-widest uppercase">

&nbsp;                               {showStatus === 'success' ? 'Message Sent Successfully!' : 'Failed to send message.'}

&nbsp;                           </span>

&nbsp;                       </div>

&nbsp;                   )}



&nbsp;                   {/\* Navbar \*/}

&nbsp;                   <nav className={`fixed w-full z-50 transition-all duration-300 ${scrolled ? 'bg-white shadow-md py-3' : 'bg-transparent py-6'}`}>

&nbsp;                       <div className="max-w-7xl mx-auto px-6 flex justify-between items-center">

&nbsp;                           <div className="flex flex-col">

&nbsp;                               <span className={`text-2xl font-bold tracking-tighter ${scrolled ? 'text-stone-800' : 'text-white'}`}>MANIKANTA</span>

&nbsp;                               <span className={`text-xs tracking-\[0.3em] font-sans font-light uppercase ${scrolled ? 'text-amber-600' : 'text-amber-400'}`}>Fine Dining</span>

&nbsp;                           </div>

&nbsp;                           <div className={`hidden md:flex space-x-10 items-center font-sans text-sm tracking-widest uppercase ${scrolled ? 'text-stone-600' : 'text-stone-100'}`}>

&nbsp;                               <a href="#home" className="hover:text-amber-500 transition">Home</a>

&nbsp;                               <a href="#menu" className="hover:text-amber-500 transition">Menu</a>

&nbsp;                               <a href="#location" className="hover:text-amber-500 transition">Location</a>

&nbsp;                               <a href="#contact" className="hover:text-amber-500 transition">Contact</a>

&nbsp;                               <button onClick={() => alert("Redirecting to Gmail...")} className={`flex items-center gap-2 border px-6 py-2 transition-all ${scrolled ? 'border-stone-800 hover:bg-stone-800 hover:text-white' : 'border-white hover:bg-white hover:text-stone-900'}`}>

&nbsp;                                   <Icon name="log-in" size={16} /> Login

&nbsp;                               </button>

&nbsp;                           </div>

&nbsp;                           <button className="md:hidden text-amber-500" onClick={() => setIsMenuOpen(!isMenuOpen)}>

&nbsp;                               <Icon name={isMenuOpen ? "x" : "menu"} />

&nbsp;                           </button>

&nbsp;                       </div>

&nbsp;                   </nav>



&nbsp;                   {/\* Mobile Menu Overlay \*/}

&nbsp;                   {isMenuOpen \&\& (

&nbsp;                       <div className="fixed inset-0 bg-stone-900 z-\[60] flex flex-col items-center justify-center space-y-8 text-white font-sans uppercase tracking-widest">

&nbsp;                           <button className="absolute top-6 right-6" onClick={() => setIsMenuOpen(false)}><Icon name="x" size={32}/></button>

&nbsp;                           <a href="#home" onClick={() => setIsMenuOpen(false)}>Home</a>

&nbsp;                           <a href="#menu" onClick={() => setIsMenuOpen(false)}>Menu</a>

&nbsp;                           <a href="#location" onClick={() => setIsMenuOpen(false)}>Location</a>

&nbsp;                           <a href="#contact" onClick={() => setIsMenuOpen(false)}>Contact</a>

&nbsp;                           <button onClick={() => alert("Redirecting...")} className="bg-amber-600 px-8 py-3">Login with Gmail</button>

&nbsp;                       </div>

&nbsp;                   )}



&nbsp;                   {/\* Hero \*/}

&nbsp;                   <section id="home" className="relative h-screen flex items-center justify-center overflow-hidden">

&nbsp;                       <div className="absolute inset-0 bg-black/50 z-10"></div>

&nbsp;                       <img src="https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?auto=format\&fit=crop\&w=1920\&q=80" alt="Fine Dining" className="absolute inset-0 w-full h-full object-cover scale-105" />

&nbsp;                       <div className="relative z-20 text-center px-6 max-w-4xl animate-fade-in">

&nbsp;                           <h1 className="text-white text-6xl md:text-8xl font-light italic mb-6 leading-tight">The Art of <span className="text-amber-400">Authentic</span> Indian Cuisine</h1>

&nbsp;                           <p className="text-stone-200 font-sans text-lg md:text-xl tracking-wide mb-10 max-w-2xl mx-auto">Experience a symphony of traditional flavors crafted with royal precision.</p>

&nbsp;                           <div className="flex flex-col sm:flex-row justify-center gap-4">

&nbsp;                               <a href="#menu" className="bg-amber-600 hover:bg-amber-700 text-white px-10 py-4 font-sans uppercase tracking-widest text-sm transition">Explore Menu</a>

&nbsp;                               <button onClick={openWhatsApp} className="border border-white hover:bg-white hover:text-stone-900 text-white px-10 py-4 font-sans uppercase tracking-widest text-sm transition">Book via WhatsApp</button>

&nbsp;                           </div>

&nbsp;                       </div>

&nbsp;                   </section>



&nbsp;                   {/\* Menu \*/}

&nbsp;                   <section id="menu" className="py-24 px-6 bg-stone-50">

&nbsp;                       <div className="max-w-7xl mx-auto">

&nbsp;                           <div className="text-center mb-16">

&nbsp;                               <h2 className="text-xs font-sans tracking-\[0.4em] text-amber-600 uppercase mb-4">Gastronomic Journey</h2>

&nbsp;                               <h3 className="text-4xl md:text-5xl font-light italic text-stone-800">Signature Selections</h3>

&nbsp;                               <div className="w-24 h-\[1px] bg-amber-400 mx-auto mt-6"></div>

&nbsp;                           </div>

&nbsp;                           <div className="flex flex-wrap justify-center gap-4 md:gap-8 mb-16">

&nbsp;                               {menuCategories.map(cat => (

&nbsp;                                   <button key={cat} onClick={() => setActiveCategory(cat)} className={`font-sans text-xs tracking-widest uppercase pb-2 transition-all border-b ${activeCategory === cat ? 'text-amber-600 border-amber-600' : 'text-stone-400 border-transparent hover:text-stone-600'}`}>{cat}</button>

&nbsp;                               ))}

&nbsp;                           </div>

&nbsp;                           <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">

&nbsp;                               {filteredMenu.map(item => (

&nbsp;                                   <div key={item.id} className="group bg-white p-8 border border-stone-100 hover:shadow-xl transition-all duration-500">

&nbsp;                                       <div className="flex justify-between items-start mb-4">

&nbsp;                                           <div>

&nbsp;                                               <span className="text-\[10px] font-sans uppercase tracking-\[0.2em] text-amber-600 mb-1 block">{item.category}</span>

&nbsp;                                               <h4 className="text-xl font-bold text-stone-800 uppercase group-hover:text-amber-600 transition-colors">{item.name}</h4>

&nbsp;                                           </div>

&nbsp;                                           <div className="text-2xl font-light text-stone-900 italic">₹{item.price}</div>

&nbsp;                                       </div>

&nbsp;                                       <p className="text-stone-500 text-sm italic mb-6 leading-relaxed">{item.description}</p>

&nbsp;                                       <div className="flex items-center justify-between mt-auto">

&nbsp;                                           <div className="flex text-amber-500 items-center"><Icon name="star" size={14} /><span className="text-xs font-sans font-bold ml-1 text-stone-600">{item.rating}</span></div>

&nbsp;                                           <button onClick={() => handleRazorpay(item.name)} className="flex items-center gap-2 font-sans text-\[10px] tracking-widest uppercase text-stone-400 hover:text-stone-800 transition"><Icon name="credit-card" size={14} /> Buy Now</button>

&nbsp;                                       </div>

&nbsp;                                   </div>

&nbsp;                               ))}

&nbsp;                           </div>

&nbsp;                       </div>

&nbsp;                   </section>



&nbsp;                   {/\* Location \& Contact Section \*/}

&nbsp;                   <section id="location" className="py-24 px-6 bg-stone-900 text-white">

&nbsp;                       <div className="max-w-7xl mx-auto">

&nbsp;                           <div className="text-center mb-16">

&nbsp;                               <h2 className="text-xs font-sans tracking-\[0.4em] text-amber-500 uppercase mb-4">Find Us</h2>

&nbsp;                               <h3 className="text-4xl md:text-5xl font-light italic">Visit Manikanta Fine Dining</h3>

&nbsp;                               <div className="w-24 h-\[1px] bg-amber-500 mx-auto mt-6"></div>

&nbsp;                           </div>

&nbsp;                           <div className="grid grid-cols-1 lg:grid-cols-2 gap-12">

&nbsp;                               <div className="h-\[450px] bg-stone-800 p-2 overflow-hidden shadow-2xl">

&nbsp;                                   <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3806.827222661234!2d78.40695007596007!3d17.420485601138814!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3bcb9135a5196387%3A0xc665b169b158f335!2sJubilee%20Hills%2C%20Hyderabad!5e0!3m2!1sen!2sin!4v1700000000000!5m2!1sen!2sin" width="100%" height="100%" frameBorder="0" allowFullScreen="" loading="lazy"></iframe>

&nbsp;                               </div>

&nbsp;                               <div id="contact" className="bg-white p-10 text-stone-900 shadow-2xl">

&nbsp;                                   <h4 className="text-2xl font-bold mb-6 uppercase tracking-tight">Enquire Now</h4>

&nbsp;                                   <p className="text-xs font-sans text-stone-500 mb-8 uppercase tracking-widest">Inquiries sent to: manikantaakula77@gmail.com</p>

&nbsp;                                   <form action="contact.php" method="POST" className="space-y-6 font-sans">

&nbsp;                                       <div className="grid grid-cols-1 md:grid-cols-2 gap-6">

&nbsp;                                           <input type="text" name="name" placeholder="Full Name" required className="w-full border-b py-3 outline-none focus:border-amber-600 transition" />

&nbsp;                                           <input type="email" name="email" placeholder="Email Address" required className="w-full border-b py-3 outline-none focus:border-amber-600 transition" />

&nbsp;                                       </div>

&nbsp;                                       <input type="text" name="subject" placeholder="Subject" required className="w-full border-b py-3 outline-none focus:border-amber-600 transition" />

&nbsp;                                       <textarea name="message" rows="4" placeholder="Your Message" required className="w-full border-b py-3 outline-none focus:border-amber-600 resize-none"></textarea>

&nbsp;                                       <button type="submit" className="w-full bg-stone-900 text-white py-4 uppercase text-xs tracking-widest hover:bg-amber-600 transition flex items-center justify-center gap-2">

&nbsp;                                           <Icon name="send" size={16} /> Send Enquiry

&nbsp;                                       </button>

&nbsp;                                   </form>

&nbsp;                               </div>

&nbsp;                           </div>

&nbsp;                       </div>

&nbsp;                   </section>



&nbsp;                   {/\* Footer \*/}

&nbsp;                   <footer className="bg-stone-50 py-20 px-6 border-t border-stone-200">

&nbsp;                       <div className="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-12">

&nbsp;                           <div>

&nbsp;                               <span className="text-3xl font-bold tracking-tighter">MANIKANTA</span><br/>

&nbsp;                               <span className="text-xs tracking-widest text-amber-600 uppercase font-sans">Fine Dining</span>

&nbsp;                               <p className="mt-6 text-stone-500 font-sans text-sm italic leading-relaxed">Experience the royal legacy of Indian cuisine, crafted with fresh ingredients and timeless traditions.</p>

&nbsp;                           </div>

&nbsp;                           <div className="space-y-4 text-stone-500 text-sm font-sans">

&nbsp;                               <h5 className="text-stone-900 font-bold uppercase tracking-widest text-xs mb-6">Contact Us</h5>

&nbsp;                               <p className="flex items-center gap-3"><Icon name="map-pin" size={18} className="text-amber-600"/> Jubilee Hills, Hyderabad</p>

&nbsp;                               <p className="flex items-center gap-3 cursor-pointer hover:text-stone-900 transition" onClick={openWhatsApp}><Icon name="phone" size={18} className="text-amber-600"/> +91 8341950743</p>

&nbsp;                               <p className="flex items-center gap-3"><Icon name="mail" size={18} className="text-amber-600"/> manikantaakula77@gmail.com</p>

&nbsp;                           </div>

&nbsp;                           <div className="space-y-6">

&nbsp;                               <h5 className="text-stone-900 font-bold uppercase tracking-widest text-xs">Follow Us</h5>

&nbsp;                               <div className="flex space-x-6">

&nbsp;                                   <Icon name="instagram" className="text-stone-400 hover:text-amber-600 cursor-pointer transition" />

&nbsp;                                   <Icon name="facebook" className="text-stone-400 hover:text-amber-600 cursor-pointer transition" />

&nbsp;                                   <Icon name="utensils" className="text-stone-400 hover:text-amber-600 cursor-pointer transition" />

&nbsp;                               </div>

&nbsp;                           </div>

&nbsp;                       </div>

&nbsp;                       <div className="text-center mt-20 border-t pt-10 font-sans text-\[10px] tracking-\[0.3em] text-stone-400 uppercase">

&nbsp;                           <p>© 2024 Manikanta Fine Dining. All Rights Reserved.</p>

&nbsp;                       </div>

&nbsp;                   </footer>

&nbsp;               </div>

&nbsp;           );

&nbsp;       };



&nbsp;       const root = ReactDOM.createRoot(document.getElementById('root'));

&nbsp;       root.render(<App />);

&nbsp;   </script>

</body>

</html>

