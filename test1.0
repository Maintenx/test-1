import React, { useState, useEffect } from 'react';
import { Plus, Search, ChevronDown, BarChart2, HardHat, Inbox, Settings, Sliders, X, AlertCircle, CheckCircle, Tool, Home, Zap } from 'lucide-react';

// Mock Data
const initialWorkOrders = [
    { id: 'WO-001', task: 'Fix leaking faucet in men\'s restroom', location: 'Building A, 2nd Floor', priority: 'High', assignedTo: 'John Doe', status: 'Open', date: '2024-07-15' },
    { id: 'WO-002', task: 'Replace faulty light fixture in main lobby', location: 'Building A, 1st Floor', priority: 'Medium', assignedTo: 'Jane Smith', status: 'In Progress', date: '2024-07-14' },
    { id: 'WO-003', task: 'HVAC unit not cooling in server room', location: 'Building B, 3rd Floor', priority: 'High', assignedTo: 'John Doe', status: 'Open', date: '2024-07-15' },
    { id: 'WO-004', task: 'Paint touch-up in Conference Room 3', location: 'Building A, 1st Floor', priority: 'Low', assignedTo: 'Emily White', status: 'Completed', date: '2024-07-12' },
    { id: 'WO-005', task: 'Unclog drain in kitchen sink', location: 'Building C, Cafeteria', priority: 'Medium', assignedTo: 'Mike Brown', status: 'In Progress', date: '2024-07-15' },
    { id: 'WO-006', task: 'Quarterly fire extinguisher inspection', location: 'All Buildings', priority: 'Medium', assignedTo: 'Jane Smith', status: 'Scheduled', date: '2024-07-20' },
    { id: 'WO-007', task: 'Repair broken window pane', location: 'Building B, Ground Floor', priority: 'High', assignedTo: 'John Doe', status: 'Completed', date: '2024-07-10' },
];

const initialInventory = [
    { id: 'INV-101', name: 'LED Light Bulbs (40W)', sku: 'LB-40W-LED', quantity: 152, location: 'Storage A', status: 'In Stock' },
    { id: 'INV-102', name: 'Air Filters (16x25x1)', sku: 'AF-16251', quantity: 45, location: 'Storage B', status: 'In Stock' },
    { id: 'INV-103', name: 'Standard Paint (White, 1 Gallon)', sku: 'PNT-WHT-1G', quantity: 12, location: 'Storage A', status: 'Low Stock' },
    { id: 'INV-104', name: 'Faucet Washer Kit', sku: 'FWK-001', quantity: 88, location: 'Storage C', status: 'In Stock' },
    { id: 'INV-105', name: 'Drywall Patch Kit', sku: 'DPK-003', quantity: 5, location: 'Storage A', status: 'Low Stock' },
    { id: 'INV-106', name: 'Cleaning Solution (All-Purpose)', sku: 'CLN-AP-5G', quantity: 20, location: 'Janitor Closet', status: 'In Stock' },
];

// Helper Components
const StatCard = ({ title, value, icon, color }) => (
    <div className="bg-white p-6 rounded-lg shadow-md flex items-center">
        <div className={`p-3 rounded-full mr-4 ${color}`}>
            {icon}
        </div>
        <div>
            <p className="text-sm font-medium text-gray-500">{title}</p>
            <p className="text-2xl font-bold text-gray-800">{value}</p>
        </div>
    </div>
);

const PriorityBadge = ({ priority }) => {
    const colors = {
        High: 'bg-red-100 text-red-800',
        Medium: 'bg-yellow-100 text-yellow-800',
        Low: 'bg-green-100 text-green-800',
    };
    return <span className={`px-2 py-1 text-xs font-semibold rounded-full ${colors[priority]}`}>{priority}</span>;
};

const StatusBadge = ({ status }) => {
    const colors = {
        Open: 'bg-blue-100 text-blue-800',
        'In Progress': 'bg-indigo-100 text-indigo-800',
        Scheduled: 'bg-purple-100 text-purple-800',
        Completed: 'bg-gray-200 text-gray-700',
    };
    return <span className={`px-2 py-1 text-xs font-semibold rounded-full ${colors[status]}`}>{status}</span>;
};

// Main Feature Components
const Dashboard = ({ workOrders, inventory }) => {
    const openOrders = workOrders.filter(o => o.status === 'Open' || o.status === 'In Progress').length;
    const completedThisMonth = workOrders.filter(o => {
        const orderDate = new Date(o.date);
        const today = new Date();
        return o.status === 'Completed' && orderDate.getMonth() === today.getMonth() && orderDate.getFullYear() === today.getFullYear();
    }).length;
    const lowStockItems = inventory.filter(i => i.status === 'Low Stock').length;
    const highPriorityTasks = workOrders.filter(o => o.priority === 'High' && o.status !== 'Completed').length;

    return (
        <div>
            <h1 className="text-3xl font-bold text-gray-800 mb-6">Dashboard</h1>
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                <StatCard title="Open Work Orders" value={openOrders} icon={<HardHat className="text-white" />} color="bg-blue-500" />
                <StatCard title="Completed This Month" value={completedThisMonth} icon={<CheckCircle className="text-white" />} color="bg-green-500" />
                <StatCard title="High Priority Tasks" value={highPriorityTasks} icon={<AlertCircle className="text-white" />} color="bg-red-500" />
                <StatCard title="Low Stock Items" value={lowStockItems} icon={<Inbox className="text-white" />} color="bg-yellow-500" />
            </div>

            <div className="bg-white p-6 rounded-lg shadow-md">
                <h2 className="text-xl font-bold text-gray-700 mb-4">Recent High-Priority Tasks</h2>
                <div className="overflow-x-auto">
                    <table className="w-full text-left">
                        <thead>
                            <tr className="border-b">
                                <th className="p-3">Task</th>
                                <th className="p-3">Location</th>
                                <th className="p-3">Assigned To</th>
                                <th className="p-3">Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            {workOrders.filter(o => o.priority === 'High').slice(0, 5).map(order => (
                                <tr key={order.id} className="border-b hover:bg-gray-50">
                                    <td className="p-3 font-medium text-gray-700">{order.task}</td>
                                    <td className="p-3 text-gray-600">{order.location}</td>
                                    <td className="p-3 text-gray-600">{order.assignedTo}</td>
                                    <td className="p-3"><StatusBadge status={order.status} /></td>
                                </tr>
                            ))}
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    );
};

const WorkOrders = ({ workOrders, setWorkOrders }) => {
    const [filter, setFilter] = useState('');
    const [isModalOpen, setIsModalOpen] = useState(false);
    const [newOrder, setNewOrder] = useState({ task: '', location: '', priority: 'Medium' });

    const filteredOrders = workOrders.filter(order =>
        order.task.toLowerCase().includes(filter.toLowerCase()) ||
        order.location.toLowerCase().includes(filter.toLowerCase()) ||
        order.assignedTo.toLowerCase().includes(filter.toLowerCase())
    );

    const handleAddOrder = (e) => {
        e.preventDefault();
        const newWorkOrder = {
            id: `WO-${String(workOrders.length + 1).padStart(3, '0')}`,
            ...newOrder,
            assignedTo: 'Unassigned',
            status: 'Open',
            date: new Date().toISOString().split('T')[0],
        };
        setWorkOrders([newWorkOrder, ...workOrders]);
        setIsModalOpen(false);
        setNewOrder({ task: '', location: '', priority: 'Medium' });
    };
    
    const handleStatusChange = (id, newStatus) => {
        setWorkOrders(workOrders.map(order => order.id === id ? { ...order, status: newStatus } : order));
    };

    return (
        <div>
            <div className="flex justify-between items-center mb-6">
                <h1 className="text-3xl font-bold text-gray-800">Work Orders</h1>
                <button onClick={() => setIsModalOpen(true)} className="bg-blue-600 text-white px-4 py-2 rounded-lg shadow hover:bg-blue-700 flex items-center transition-colors">
                    <Plus size={20} className="mr-2" /> New Work Order
                </button>
            </div>

            <div className="bg-white p-4 rounded-lg shadow-md mb-6">
                <div className="relative">
                    <Search size={20} className="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" />
                    <input
                        type="text"
                        placeholder="Search orders by task, location, assignee..."
                        className="w-full pl-10 pr-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                        value={filter}
                        onChange={(e) => setFilter(e.target.value)}
                    />
                </div>
            </div>

            <div className="bg-white rounded-lg shadow-md overflow-hidden">
                <div className="overflow-x-auto">
                    <table className="w-full text-left">
                        <thead className="bg-gray-50">
                            <tr className="border-b">
                                <th className="p-4 font-semibold text-gray-600">ID</th>
                                <th className="p-4 font-semibold text-gray-600">Task</th>
                                <th className="p-4 font-semibold text-gray-600">Location</th>
                                <th className="p-4 font-semibold text-gray-600">Priority</th>
                                <th className="p-4 font-semibold text-gray-600">Assigned To</th>
                                <th className="p-4 font-semibold text-gray-600">Date</th>
                                <th className="p-4 font-semibold text-gray-600">Status</th>
                                <th className="p-4 font-semibold text-gray-600">Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            {filteredOrders.map(order => (
                                <tr key={order.id} className="border-b hover:bg-gray-50">
                                    <td className="p-4 text-sm text-gray-500">{order.id}</td>
                                    <td className="p-4 font-medium text-gray-800">{order.task}</td>
                                    <td className="p-4 text-gray-600">{order.location}</td>
                                    <td className="p-4"><PriorityBadge priority={order.priority} /></td>
                                    <td className="p-4 text-gray-600">{order.assignedTo}</td>
                                    <td className="p-4 text-gray-600">{order.date}</td>
                                    <td className="p-4"><StatusBadge status={order.status} /></td>
                                    <td className="p-4">
                                        <select 
                                            value={order.status} 
                                            onChange={(e) => handleStatusChange(order.id, e.target.value)}
                                            className="border rounded-md p-1 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
                                        >
                                            <option>Open</option>
                                            <option>In Progress</option>
                                            <option>Scheduled</option>
                                            <option>Completed</option>
                                        </select>
                                    </td>
                                </tr>
                            ))}
                        </tbody>
                    </table>
                </div>
            </div>

            {isModalOpen && (
                <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
                    <div className="bg-white p-8 rounded-lg shadow-2xl w-full max-w-md">
                        <div className="flex justify-between items-center mb-6">
                            <h2 className="text-2xl font-bold text-gray-800">New Work Order</h2>
                            <button onClick={() => setIsModalOpen(false)} className="text-gray-500 hover:text-gray-800">
                                <X size={24} />
                            </button>
                        </div>
                        <form onSubmit={handleAddOrder}>
                            <div className="mb-4">
                                <label className="block text-sm font-medium text-gray-700 mb-1">Task Description</label>
                                <input type="text" value={newOrder.task} onChange={e => setNewOrder({...newOrder, task: e.target.value})} className="w-full p-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" required />
                            </div>
                            <div className="mb-4">
                                <label className="block text-sm font-medium text-gray-700 mb-1">Location</label>
                                <input type="text" value={newOrder.location} onChange={e => setNewOrder({...newOrder, location: e.target.value})} className="w-full p-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" required />
                            </div>
                            <div className="mb-6">
                                <label className="block text-sm font-medium text-gray-700 mb-1">Priority</label>
                                <select value={newOrder.priority} onChange={e => setNewOrder({...newOrder, priority: e.target.value})} className="w-full p-2 border rounded-md bg-white focus:outline-none focus:ring-2 focus:ring-blue-500">
                                    <option>Low</option>
                                    <option>Medium</option>
                                    <option>High</option>
                                </select>
                            </div>
                            <div className="flex justify-end">
                                <button type="button" onClick={() => setIsModalOpen(false)} className="mr-4 px-4 py-2 text-gray-700 bg-gray-100 rounded-lg hover:bg-gray-200">Cancel</button>
                                <button type="submit" className="px-4 py-2 bg-blue-600 text-white rounded-lg shadow hover:bg-blue-700">Create Order</button>
                            </div>
                        </form>
                    </div>
                </div>
            )}
        </div>
    );
};

const Inventory = ({ inventory, setInventory }) => {
    const [isModalOpen, setIsModalOpen] = useState(false);
    const [newItem, setNewItem] = useState({ name: '', sku: '', quantity: '', location: '' });

    const handleAddItem = (e) => {
        e.preventDefault();
        const newInventoryItem = {
            id: `INV-${String(inventory.length + 107).padStart(3, '0')}`,
            ...newItem,
            quantity: parseInt(newItem.quantity),
            status: parseInt(newItem.quantity) > 15 ? 'In Stock' : 'Low Stock',
        };
        setInventory([newInventoryItem, ...inventory]);
        setIsModalOpen(false);
        setNewItem({ name: '', sku: '', quantity: '', location: '' });
    };

    return (
        <div>
            <div className="flex justify-between items-center mb-6">
                <h1 className="text-3xl font-bold text-gray-800">Inventory</h1>
                <button onClick={() => setIsModalOpen(true)} className="bg-blue-600 text-white px-4 py-2 rounded-lg shadow hover:bg-blue-700 flex items-center transition-colors">
                    <Plus size={20} className="mr-2" /> Add New Item
                </button>
            </div>
            <div className="bg-white rounded-lg shadow-md overflow-hidden">
                <div className="overflow-x-auto">
                    <table className="w-full text-left">
                        <thead className="bg-gray-50">
                            <tr className="border-b">
                                <th className="p-4 font-semibold text-gray-600">Item Name</th>
                                <th className="p-4 font-semibold text-gray-600">SKU</th>
                                <th className="p-4 font-semibold text-gray-600">Quantity</th>
                                <th className="p-4 font-semibold text-gray-600">Location</th>
                                <th className="p-4 font-semibold text-gray-600">Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            {inventory.map(item => (
                                <tr key={item.id} className="border-b hover:bg-gray-50">
                                    <td className="p-4 font-medium text-gray-800">{item.name}</td>
                                    <td className="p-4 text-gray-600">{item.sku}</td>
                                    <td className="p-4 text-gray-600">{item.quantity}</td>
                                    <td className="p-4 text-gray-600">{item.location}</td>
                                    <td className="p-4">
                                        <span className={`px-2 py-1 text-xs font-semibold rounded-full ${item.status === 'In Stock' ? 'bg-green-100 text-green-800' : 'bg-yellow-100 text-yellow-800'}`}>
                                            {item.status}
                                        </span>
                                    </td>
                                </tr>
                            ))}
                        </tbody>
                    </table>
                </div>
            </div>

            {isModalOpen && (
                <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
                    <div className="bg-white p-8 rounded-lg shadow-2xl w-full max-w-md">
                        <div className="flex justify-between items-center mb-6">
                            <h2 className="text-2xl font-bold text-gray-800">New Inventory Item</h2>
                            <button onClick={() => setIsModalOpen(false)} className="text-gray-500 hover:text-gray-800">
                                <X size={24} />
                            </button>
                        </div>
                        <form onSubmit={handleAddItem}>
                            <div className="mb-4">
                                <label className="block text-sm font-medium text-gray-700 mb-1">Item Name</label>
                                <input type="text" value={newItem.name} onChange={e => setNewItem({...newItem, name: e.target.value})} className="w-full p-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" required />
                            </div>
                            <div className="mb-4">
                                <label className="block text-sm font-medium text-gray-700 mb-1">SKU</label>
                                <input type="text" value={newItem.sku} onChange={e => setNewItem({...newItem, sku: e.target.value})} className="w-full p-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" required />
                            </div>
                            <div className="mb-4">
                                <label className="block text-sm font-medium text-gray-700 mb-1">Quantity</label>
                                <input type="number" value={newItem.quantity} onChange={e => setNewItem({...newItem, quantity: e.target.value})} className="w-full p-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" required />
                            </div>
                            <div className="mb-6">
                                <label className="block text-sm font-medium text-gray-700 mb-1">Storage Location</label>
                                <input type="text" value={newItem.location} onChange={e => setNewItem({...newItem, location: e.target.value})} className="w-full p-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" required />
                            </div>
                            <div className="flex justify-end">
                                <button type="button" onClick={() => setIsModalOpen(false)} className="mr-4 px-4 py-2 text-gray-700 bg-gray-100 rounded-lg hover:bg-gray-200">Cancel</button>
                                <button type="submit" className="px-4 py-2 bg-blue-600 text-white rounded-lg shadow hover:bg-blue-700">Add Item</button>
                            </div>
                        </form>
                    </div>
                </div>
            )}
        </div>
    );
};

const PlaceholderPage = ({ title, icon }) => (
    <div>
        <h1 className="text-3xl font-bold text-gray-800 mb-6">{title}</h1>
        <div className="bg-white p-12 rounded-lg shadow-md text-center">
            <div className="flex justify-center mb-4 text-blue-500">
                {icon}
            </div>
            <h2 className="text-xl font-semibold text-gray-700 mb-2">Feature Coming Soon</h2>
            <p className="text-gray-500">This section is under development. Check back later for updates!</p>
        </div>
    </div>
);


// Main App Component
export default function App() {
    const [activePage, setActivePage] = useState('Dashboard');
    const [workOrders, setWorkOrders] = useState(initialWorkOrders);
    const [inventory, setInventory] = useState(initialInventory);
    const [isSidebarOpen, setIsSidebarOpen] = useState(true);

    const NavItem = ({ page, icon, children }) => (
        <li
            onClick={() => setActivePage(page)}
            className={`flex items-center p-3 my-1 rounded-lg cursor-pointer transition-colors ${
                activePage === page ? 'bg-blue-600 text-white shadow-lg' : 'text-gray-600 hover:bg-gray-200'
            }`}
        >
            {icon}
            <span className={`ml-4 font-medium ${isSidebarOpen ? 'inline' : 'hidden'}`}>{children}</span>
        </li>
    );

    const renderPage = () => {
        switch (activePage) {
            case 'Dashboard':
                return <Dashboard workOrders={workOrders} inventory={inventory} />;
            case 'Work Orders':
                return <WorkOrders workOrders={workOrders} setWorkOrders={setWorkOrders} />;
            case 'Inventory':
                return <Inventory inventory={inventory} setInventory={setInventory} />;
            case 'Reports':
                return <PlaceholderPage title="Reports" icon={<BarChart2 size={48} />} />;
            case 'Settings':
                return <PlaceholderPage title="Settings" icon={<Settings size={48} />} />;
            default:
                return <Dashboard />;
        }
    };

    return (
        <div className="flex h-screen bg-gray-100 font-sans">
            {/* Sidebar */}
            <aside className={`bg-white text-gray-800 transition-all duration-300 ease-in-out ${isSidebarOpen ? 'w-64' : 'w-20'} flex flex-col`}>
                <div className="flex items-center justify-between p-4 border-b h-16">
                    <div className={`flex items-center ${isSidebarOpen ? 'opacity-100' : 'opacity-0'}`}>
                        <Zap className="text-blue-600" size={28} />
                        <h1 className="text-xl font-bold ml-2">MaintenX</h1>
                    </div>
                    <button onClick={() => setIsSidebarOpen(!isSidebarOpen)} className="p-2 rounded-lg hover:bg-gray-200">
                        <Sliders size={20} />
                    </button>
                </div>
                <nav className="flex-1 p-4">
                    <ul>
                        <NavItem page="Dashboard" icon={<Home size={20} />}>Dashboard</NavItem>
                        <NavItem page="Work Orders" icon={<HardHat size={20} />}>Work Orders</NavItem>
                        <NavItem page="Inventory" icon={<Inbox size={20} />}>Inventory</NavItem>
                        <NavItem page="Reports" icon={<BarChart2 size={20} />}>Reports</NavItem>
                        <NavItem page="Settings" icon={<Settings size={20} />}>Settings</NavItem>
                    </ul>
                </nav>
                <div className="p-4 border-t">
                    <div className="flex items-center">
                        <img src="https://placehold.co/40x40/E2E8F0/4A5568?text=JD" alt="User Avatar" className="rounded-full" />
                        <div className={`ml-3 ${isSidebarOpen ? 'inline' : 'hidden'}`}>
                            <p className="font-semibold text-sm">John Doe</p>
                            <p className="text-xs text-gray-500">Technician</p>
                        </div>
                    </div>
                </div>
            </aside>

            {/* Main Content */}
            <main className="flex-1 p-6 lg:p-10 overflow-y-auto">
                {renderPage()}
            </main>
        </div>
    );
}
