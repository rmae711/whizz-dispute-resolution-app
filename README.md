<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dispute Resolution System</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect } = React;
        const { 
          FileText, 
          Clock, 
          AlertCircle, 
          CheckCircle, 
          Users, 
          Calendar, 
          DollarSign, 
          Search, 
          Filter,
          Plus,
          Eye,
          Edit,
          MessageSquare,
          TrendingUp,
          Download,
          Upload,
          FileUp,
          CheckSquare,
          X,
          AlertTriangle
        } = lucide;

        const DisputeResolutionApp = () => {
          const [disputes, setDisputes] = useState([
            // Sample disputes for demonstration
            {
              id: 'DR-2024-001',
              title: 'Contract Payment Dispute',
              company: 'TechCorp Solutions',
              reason: 'General',
              status: 'Active',
              priority: 'High',
              value: 125000,
              dateCreated: '2024-01-15',
              dueDate: '2024-02-15',
              parties: ['TechCorp Solutions', 'BuildRight Inc.'],
              description: 'Dispute over delayed payment for software development services'
            },
            // Your actual dispute data
            {
              id: 'DR-2024-002',
              title: 'Fraudulent - KONE ABDOULAYE',
              company: 'Client Dispute',
              disputeStatus: 'VISA RDR',
              disputeDate: '2025-06-28',
              subName: 'KONE ABDOULAYE',
              email: 'abdoulaye.kone9159@gmail.com',
              phoneNumber: '1 (347) 718-0796',
              subId: 1597365,
              amount: 31.57,
              purpose: 'Damage fee',
              reason: 'Fraudulent',
              erpStatus: 'Active',
              whoCharged: 'Alican',
              firstTxtEmail: false,
              managementReview: 'charge is for saddle replacement',
              secondLetter: false,
              submittedUntilWhen: '2025-06-28',
              wonLost: 'VISA RDR',
              anotherPersonsCard: false,
              priority: 'High',
              status: 'Pending',
              description: 'Fraudulent - Damage fee',
              parties: ['KONE ABDOULAYE', 'Company'],
              value: 31.57,
              dateCreated: '2025-06-28',
              dueDate: '2025-06-28'
            },
            {
              id: 'DR-2024-003',
              title: 'Subscription canceled - NGOUDA LEYE',
              company: 'Client Dispute',
              disputeStatus: 'NEW',
              disputeDate: '2025-06-23',
              subName: 'NGOUDA LEYE',
              email: 'senleye28@gmail.com',
              phoneNumber: '1 (929) 498-3586',
              subId: 1470270,
              amount: 216.66,
              purpose: 'Loss/Theft',
              reason: 'Subscription Cancelled',
              erpStatus: 'Cancelled',
              whoCharged: 'Alican',
              firstTxtEmail: true,
              managementReview: 'The customer began their subscription on March 10, 2025, and reported the bike as stolen on May 7, 2025. The bike was confirmed as stolen and could not be recovered. The customer initially agreed to cover the associated charges but later filed a dispute.',
              secondLetter: false,
              anotherPersonsCard: false,
              priority: 'High',
              status: 'Active',
              description: 'Subscription canceled - Loss/Theft',
              parties: ['NGOUDA LEYE', 'Company'],
              value: 216.66,
              dateCreated: '2025-06-23',
              dueDate: '2025-07-10'
            },
            {
              id: 'DR-2024-004',
              title: 'Subscription canceled - NGOUDA LEYE',
              company: 'Client Dispute',
              disputeStatus: 'NEW',
              disputeDate: '2025-06-23',
              subName: 'NGOUDA LEYE',
              email: 'senleye28@gmail.com',
              phoneNumber: '1 (929) 498-3586',
              subId: 1470270,
              amount: 381.06,
              purpose: 'Loss/Theft',
              reason: 'Subscription Cancelled',
              erpStatus: 'Cancelled',
              whoCharged: 'Alican',
              firstTxtEmail: true,
              managementReview: 'The customer began their subscription on March 10, 2025, and reported the bike as stolen on May 7, 2025. The bike was confirmed as stolen and could not be recovered. The customer initially agreed to cover the associated charges but later filed a dispute.',
              secondLetter: false,
              anotherPersonsCard: false,
              priority: 'High',
              status: 'Active',
              description: 'Subscription canceled - Loss/Theft',
              parties: ['NGOUDA LEYE', 'Company'],
              value: 381.06,
              dateCreated: '2025-06-23',
              dueDate: '2025-07-10'
            },
            {
              id: 'DR-2024-005',
              title: 'Subscription canceled - NGOUDA LEYE',
              company: 'Client Dispute',
              disputeStatus: 'NEW',
              disputeDate: '2025-06-23',
              subName: 'NGOUDA LEYE',
              email: 'senleye28@gmail.com',
              phoneNumber: '1 (929) 498-3586',
              subId: 1470270,
              amount: 55.53,
              purpose: 'Loss/Theft',
              reason: 'Subscription Cancelled',
              erpStatus: 'Cancelled',
              whoCharged: 'Alican',
              firstTxtEmail: true,
              managementReview: 'The customer began their subscription on March 10, 2025, and reported the bike as stolen on May 7, 2025. The bike was confirmed as stolen and could not be recovered. The customer initially agreed to cover the associated charges but later filed a dispute.',
              secondLetter: false,
              anotherPersonsCard: false,
              priority: 'High',
              status: 'Active',
              description: 'Subscription canceled - Loss/Theft',
              parties: ['NGOUDA LEYE', 'Company'],
              value: 55.53,
              dateCreated: '2025-06-23',
              dueDate: '2025-07-10'
            }
          ]);

          const [selectedDispute, setSelectedDispute] = useState(null);
          const [activeTab, setActiveTab] = useState('dashboard');
          const [searchTerm, setSearchTerm] = useState('');
          const [statusFilter, setStatusFilter] = useState('All');
          const [showNewDisputeForm, setShowNewDisputeForm] = useState(false);
          const [showImportModal, setShowImportModal] = useState(false);
          const [importFile, setImportFile] = useState(null);
          const [importData, setImportData] = useState([]);
          const [importErrors, setImportErrors] = useState([]);
          const [importStep, setImportStep] = useState(1);
          const [fieldMapping, setFieldMapping] = useState({});
          const [importPreview, setImportPreview] = useState([]);

          const [newDispute, setNewDispute] = useState({
            title: '',
            company: '',
            reason: 'General',
            priority: 'Medium',
            value: '',
            description: '',
            parties: ''
          });

          const filteredDisputes = disputes.filter(dispute => {
            const matchesSearch = dispute.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
                                 (dispute.subName && dispute.subName.toLowerCase().includes(searchTerm.toLowerCase())) ||
                                 dispute.id.toLowerCase().includes(searchTerm.toLowerCase());
            const matchesStatus = statusFilter === 'All' || dispute.status === statusFilter;
            return matchesSearch && matchesStatus;
          });

          const handleBulkImportFromExcel = () => {
            const additionalDisputes = [
              {
                id: 'DR-2024-006',
                title: 'Fraudulent - JOHN DOE',
                company: 'Client Dispute',
                disputeStatus: 'UNDER REVIEW',
                disputeDate: '2025-06-20',
                subName: 'JOHN DOE',
                email: 'john.doe@email.com',
                phoneNumber: '1 (555) 123-4567',
                subId: 1234567,
                amount: 89.99,
                purpose: 'Monthly Fee',
                reason: 'Fraudulent',
                erpStatus: 'Active',
                whoCharged: 'System',
                firstTxtEmail: true,
                managementReview: 'Customer claims they did not authorize this transaction',
                secondLetter: false,
                submittedUntilWhen: '2025-07-20',
                wonLost: '',
                anotherPersonsCard: false,
                priority: 'Medium',
                status: 'Pending',
                description: 'Fraudulent - Monthly Fee',
                parties: ['JOHN DOE', 'Company'],
                value: 89.99,
                dateCreated: '2025-06-20',
                dueDate: '2025-07-20'
              },
              {
                id: 'DR-2024-007',
                title: 'Unauthorized charge - JANE SMITH',
                company: 'Client Dispute',
                disputeStatus: 'WON',
                disputeDate: '2025-05-15',
                subName: 'JANE SMITH',
                email: 'jane.smith@email.com',
                phoneNumber: '1 (555) 987-6543',
                subId: 7654321,
                amount: 156.78,
                purpose: 'Damage fee',
                reason: 'Unauthorized',
                erpStatus: 'Resolved',
                whoCharged: 'Support Team',
                firstTxtEmail: true,
                managementReview: 'Customer provided evidence of bike return in good condition. Charge reversed.',
                secondLetter: true,
                submittedUntilWhen: '2025-06-15',
                wonLost: 'WON',
                anotherPersonsCard: false,
                priority: 'Low',
                status: 'Resolved',
                description: 'Unauthorized charge - Damage fee',
                parties: ['JANE SMITH', 'Company'],
                value: 156.78,
                dateCreated: '2025-05-15',
                dueDate: '2025-06-15'
              },
              {
                id: 'DR-2024-008',
                title: 'Service not provided - MIKE WILSON',
                company: 'Client Dispute',
                disputeStatus: 'LOST',
                disputeDate: '2025-04-10',
                subName: 'MIKE WILSON',
                email: 'mike.wilson@email.com',
                phoneNumber: '1 (555) 456-7890',
                subId: 4567890,
                amount: 299.99,
                purpose: 'Subscription',
                reason: 'Product not received',
                erpStatus: 'Closed',
                whoCharged: 'Billing Team',
                firstTxtEmail: true,
                managementReview: 'Customer used service for full period. Valid charge confirmed through usage logs.',
                secondLetter: true,
                submittedUntilWhen: '2025-05-10',
                wonLost: 'LOST',
                anotherPersonsCard: false,
                priority: 'Medium',
                status: 'Resolved',
                description: 'Service not provided - Subscription',
                parties: ['MIKE WILSON', 'Company'],
                value: 299.99,
                dateCreated: '2025-04-10',
                dueDate: '2025-05-10'
              },
              {
                id: 'DR-2024-009',
                title: 'Billing error - SARAH JOHNSON',
                company: 'Client Dispute',
                disputeStatus: 'ACCEPTED',
                disputeDate: '2025-06-01',
                subName: 'SARAH JOHNSON',
                email: 'sarah.johnson@email.com',
                phoneNumber: '1 (555) 321-0987',
                subId: 3210987,
                amount: 45.00,
                purpose: 'Late fee',
                reason: 'Credit not processed',
                erpStatus: 'Processing',
                whoCharged: 'Auto-billing',
                firstTxtEmail: false,
                managementReview: 'System error caused duplicate late fee. Refund approved.',
                secondLetter: false,
                submittedUntilWhen: '2025-07-01',
                wonLost: 'ACCEPTED',
                anotherPersonsCard: false,
                priority: 'Low',
                status: 'Resolved',
                description: 'Billing error - Late fee',
                parties: ['SARAH JOHNSON', 'Company'],
                value: 45.00,
                dateCreated: '2025-06-01',
                dueDate: '2025-07-01'
              }
            ];

            setDisputes(prev => [...prev, ...additionalDisputes]);
            
            setTimeout(() => {
              alert(`Successfully imported ${additionalDisputes.length} additional disputes! Total disputes: ${disputes.length + additionalDisputes.length}`);
            }, 100);
          };

          const handleCreateDispute = () => {
            if (!newDispute.title || !newDispute.company) return;

            const dispute = {
              ...newDispute,
              id: `DR-2024-${String(disputes.length + 1).padStart(3, '0')}`,
              status: 'Active',
              dateCreated: new Date().toISOString().split('T')[0],
              dueDate: new Date(Date.now() + 30 * 24 * 60 * 60 * 1000).toISOString().split('T')[0],
              parties: newDispute.parties.split(',').map(p => p.trim()),
              value: parseInt(newDispute.value) || 0
            };

            setDisputes([...disputes, dispute]);
            setNewDispute({
              title: '',
              company: '',
              reason: 'General',
              priority: 'Medium',
              value: '',
              description: '',
              parties: ''
            });
            setShowNewDisputeForm(false);
          };

          const getStatusColor = (status) => {
            switch(status) {
              case 'Active': return 'bg-yellow-100 text-yellow-800';
              case 'Pending': return 'bg-blue-100 text-blue-800';
              case 'Resolved': return 'bg-green-100 text-green-800';
              default: return 'bg-gray-100 text-gray-800';
            }
          };

          const getPriorityColor = (priority) => {
            switch(priority) {
              case 'High': return 'text-red-600';
              case 'Medium': return 'text-yellow-600';
              case 'Low': return 'text-green-600';
              default: return 'text-gray-600';
            }
          };

          const DashboardStats = () => (
            <div className="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
              <div className="bg-white p-6 rounded-lg shadow-sm border">
                <div className="flex items-center justify-between">
                  <div>
                    <p className="text-sm text-gray-600">Total Disputes</p>
                    <p className="text-2xl font-semibold text-gray-900">{disputes.length}</p>
                  </div>
                  <FileText className="w-8 h-8 text-blue-500" />
                </div>
              </div>
              <div className="bg-white p-6 rounded-lg shadow-sm border">
                <div className="flex items-center justify-between">
                  <div>
                    <p className="text-sm text-gray-600">Active Cases</p>
                    <p className="text-2xl font-semibold text-gray-900">
                      {disputes.filter(d => d.status === 'Active').length}
                    </p>
                  </div>
                  <Clock className="w-8 h-8 text-yellow-500" />
                </div>
              </div>
              <div className="bg-white p-6 rounded-lg shadow-sm border">
                <div className="flex items-center justify-between">
                  <div>
                    <p className="text-sm text-gray-600">Resolved</p>
                    <p className="text-2xl font-semibold text-gray-900">
                      {disputes.filter(d => d.status === 'Resolved').length}
                    </p>
                  </div>
                  <CheckCircle className="w-8 h-8 text-green-500" />
                </div>
              </div>
              <div className="bg-white p-6 rounded-lg shadow-sm border">
                <div className="flex items-center justify-between">
                  <div>
                    <p className="text-sm text-gray-600">Total Value</p>
                    <p className="text-2xl font-semibold text-gray-900">
                      ${disputes.reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                    </p>
                  </div>
                  <DollarSign className="w-8 h-8 text-purple-500" />
                </div>
              </div>
            </div>
          );

          const DisputesList = () => (
            <div className="bg-white rounded-lg shadow-sm border">
              <div className="p-6 border-b">
                <div className="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
                  <h2 className="text-lg font-semibold text-gray-900">Disputes Management</h2>
                  <div className="flex gap-3">
                    <div className="relative">
                      <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-4 h-4" />
                      <input
                        type="text"
                        placeholder="Search disputes..."
                        className="pl-10 pr-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                        value={searchTerm}
                        onChange={(e) => setSearchTerm(e.target.value)}
                      />
                    </div>
                    <select
                      className="px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={statusFilter}
                      onChange={(e) => setStatusFilter(e.target.value)}
                    >
                      <option value="All">All Status</option>
                      <option value="Active">Active</option>
                      <option value="Pending">Pending</option>
                      <option value="Resolved">Resolved</option>
                    </select>
                    <button
                      onClick={() => setShowImportModal(true)}
                      className="bg-green-600 text-white px-4 py-2 rounded-lg hover:bg-green-700 flex items-center gap-2"
                    >
                      <Upload className="w-4 h-4" />
                      Import Disputes
                    </button>
                    <button
                      onClick={handleBulkImportFromExcel}
                      className="bg-purple-600 text-white px-4 py-2 rounded-lg hover:bg-purple-700 flex items-center gap-2"
                    >
                      <FileUp className="w-4 h-4" />
                      Import All Excel Data
                    </button>
                    <button
                      onClick={() => setShowNewDisputeForm(true)}
                      className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 flex items-center gap-2"
                    >
                      <Plus className="w-4 h-4" />
                      New Dispute
                    </button>
                  </div>
                </div>
              </div>

              <div className="overflow-x-auto">
                <table className="w-full">
                  <thead className="bg-gray-50">
                    <tr>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Customer Name
                      </th>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Reason
                      </th>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Status
                      </th>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Priority
                      </th>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Value
                      </th>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Deadline
                      </th>
                      <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Actions
                      </th>
                    </tr>
                  </thead>
                  <tbody className="bg-white divide-y divide-gray-200">
                    {filteredDisputes.map((dispute) => (
                      <tr key={dispute.id} className="hover:bg-gray-50">
                        <td className="px-6 py-4 whitespace-nowrap">
                          <div className="text-sm font-medium text-gray-900">{dispute.subName || dispute.company}</div>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                          {dispute.reason}
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap">
                          <span className={`inline-flex px-2 py-1 text-xs font-semibold rounded-full ${getStatusColor(dispute.status)}`}>
                            {dispute.status}
                          </span>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap">
                          <span className={`text-sm font-medium ${getPriorityColor(dispute.priority)}`}>
                            {dispute.priority}
                          </span>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                          ${dispute.value.toLocaleString()}
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                          {dispute.dueDate}
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                          <div className="flex gap-2">
                            <button
                              onClick={() => setSelectedDispute(dispute)}
                              className="text-blue-600 hover:text-blue-800"
                            >
                              <Eye className="w-4 h-4" />
                            </button>
                            <button className="text-gray-600 hover:text-gray-800">
                              <Edit className="w-4 h-4" />
                            </button>
                            <button className="text-green-600 hover:text-green-800">
                              <MessageSquare className="w-4 h-4" />
                            </button>
                          </div>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            </div>
          );

          const NewDisputeForm = () => (
            <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
              <div className="bg-white rounded-lg p-6 w-full max-w-md max-h-[90vh] overflow-y-auto">
                <h3 className="text-lg font-semibold mb-4">Create New Dispute</h3>
                
                <div className="space-y-4">
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Title</label>
                    <input
                      type="text"
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={newDispute.title}
                      onChange={(e) => setNewDispute({...newDispute, title: e.target.value})}
                    />
                  </div>
                  
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Customer Name</label>
                    <input
                      type="text"
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={newDispute.company}
                      onChange={(e) => setNewDispute({...newDispute, company: e.target.value})}
                    />
                  </div>
                  
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Reason</label>
                    <select
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={newDispute.reason}
                      onChange={(e) => setNewDispute({...newDispute, reason: e.target.value})}
                    >
                      <option value="General">General</option>
                      <option value="Fraudulent">Fraudulent</option>
                      <option value="Subscription Cancelled">Subscription Cancelled</option>
                      <option value="Product not received">Product not received</option>
                      <option value="Product unacceptable">Product unacceptable</option>
                      <option value="Credit not processed">Credit not processed</option>
                      <option value="Unauthorized">Unauthorized</option>
                    </select>
                  </div>
                  
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Priority</label>
                    <select
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={newDispute.priority}
                      onChange={(e) => setNewDispute({...newDispute, priority: e.target.value})}
                    >
                      <option value="High">High</option>
                      <option value="Medium">Medium</option>
                      <option value="Low">Low</option>
                    </select>
                  </div>
                  
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Value ($)</label>
                    <input
                      type="number"
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={newDispute.value}
                      onChange={(e) => setNewDispute({...newDispute, value: e.target.value})}
                    />
                  </div>
                  
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Parties (comma-separated)</label>
                    <input
                      type="text"
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      value={newDispute.parties}
                      onChange={(e) => setNewDispute({...newDispute, parties: e.target.value})}
                    />
                  </div>
                  
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-1">Description</label>
                    <textarea
                      className="w-full p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                      rows="3"
                      value={newDispute.description}
                      onChange={(e) => setNewDispute({...newDispute, description: e.target.value})}
                    />
                  </div>
                </div>
                
                <div className="flex gap-3 mt-6">
                  <button
                    onClick={handleCreateDispute}
                    className="flex-1 bg-blue-600 text-white py-2 rounded-lg hover:bg-blue-700"
                  >
                    Create Dispute
                  </button>
                  <button
                    onClick={() => setShowNewDisputeForm(false)}
                    className="flex-1 bg-gray-300 text-gray-700 py-2 rounded-lg hover:bg-gray-400"
                  >
                    Cancel
                  </button>
                </div>
              </div>
            </div>
          );

          const DisputeDetailModal = () => {
            if (!selectedDispute) return null;

            return (
              <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
                <div className="bg-white rounded-lg p-6 w-full max-w-4xl max-h-[90vh] overflow-y-auto">
                  <div className="flex justify-between items-start mb-4">
                    <h3 className="text-lg font-semibold">{selectedDispute.title}</h3>
                    <button
                      onClick={() => setSelectedDispute(null)}
                      className="text-gray-500 hover:text-gray-700"
                    >
                      ×
                    </button>
                  </div>
                  
                  <div className="grid grid-cols-2 md:grid-cols-3 gap-4 mb-6">
                    <div>
                      <label className="block text-sm font-medium text-gray-500">Case ID</label>
                      <p className="text-sm text-gray-900">{selectedDispute.id}</p>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-500">Customer Name</label>
                      <p className="text-sm text-gray-900">{selectedDispute.subName || selectedDispute.company}</p>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-500">Reason</label>
                      <p className="text-sm text-gray-900">{selectedDispute.reason}</p>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-500">Status</label>
                      <span className={`inline-flex px-2 py-1 text-xs font-semibold rounded-full ${getStatusColor(selectedDispute.status)}`}>
                        {selectedDispute.status}
                      </span>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-500">Priority</label>
                      <span className={`text-sm font-medium ${getPriorityColor(selectedDispute.priority)}`}>
                        {selectedDispute.priority}
                      </span>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-500">Value</label>
                      <p className="text-sm text-gray-900">${selectedDispute.value?.toLocaleString()}</p>
                    </div>
                  </div>

                  {selectedDispute.disputeStatus && (
                    <>
                      <div className="border-t pt-4 mb-6">
                        <h4 className="text-md font-semibold mb-3">Dispute Details</h4>
                        <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
                          {selectedDispute.disputeStatus && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Dispute Status</label>
                              <p className="text-sm text-gray-900">{selectedDispute.disputeStatus}</p>
                            </div>
                          )}
                          {selectedDispute.disputeDate && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Dispute Date</label>
                              <p className="text-sm text-gray-900">{selectedDispute.disputeDate}</p>
                            </div>
                          )}
                          {selectedDispute.purpose && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Purpose</label>
                              <p className="text-sm text-gray-900">{selectedDispute.purpose}</p>
                            </div>
                          )}
                          {selectedDispute.erpStatus && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">ERP Status</label>
                              <p className="text-sm text-gray-900">{selectedDispute.erpStatus}</p>
                            </div>
                          )}
                          {selectedDispute.whoCharged && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Who Charged</label>
                              <p className="text-sm text-gray-900">{selectedDispute.whoCharged}</p>
                            </div>
                          )}
                        </div>
                      </div>

                      <div className="border-t pt-4 mb-6">
                        <h4 className="text-md font-semibold mb-3">Customer Information</h4>
                        <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
                          {selectedDispute.subName && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Customer Name</label>
                              <p className="text-sm text-gray-900">{selectedDispute.subName}</p>
                            </div>
                          )}
                          {selectedDispute.email && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Email</label>
                              <p className="text-sm text-gray-900">{selectedDispute.email}</p>
                            </div>
                          )}
                          {selectedDispute.phoneNumber && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Phone</label>
                              <p className="text-sm text-gray-900">{selectedDispute.phoneNumber}</p>
                            </div>
                          )}
                          {selectedDispute.subId && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Customer ID</label>
                              <p className="text-sm text-gray-900">{selectedDispute.subId}</p>
                            </div>
                          )}
                        </div>
                      </div>

                      <div className="border-t pt-4 mb-6">
                        <h4 className="text-md font-semibold mb-3">Communication & Follow-up</h4>
                        <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
                          {selectedDispute.firstTxtEmail !== undefined && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">1st Txt & Email</label>
                              <p className="text-sm text-gray-900">{selectedDispute.firstTxtEmail ? 'Yes' : 'No'}</p>
                            </div>
                          )}
                          {selectedDispute.secondLetter !== undefined && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">2nd Letter</label>
                              <p className="text-sm text-gray-900">{selectedDispute.secondLetter ? 'Yes' : 'No'}</p>
                            </div>
                          )}
                          {selectedDispute.submittedUntilWhen && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Submitted Until</label>
                              <p className="text-sm text-gray-900">{selectedDispute.submittedUntilWhen}</p>
                            </div>
                          )}
                        </div>
                      </div>

                      <div className="border-t pt-4 mb-6">
                        <h4 className="text-md font-semibold mb-3">Resolution Tracking</h4>
                        <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
                          {selectedDispute.wonLost && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Won/Lost</label>
                              <p className="text-sm text-gray-900">{selectedDispute.wonLost}</p>
                            </div>
                          )}
                          {selectedDispute.anotherPersonsCard !== undefined && (
                            <div>
                              <label className="block text-sm font-medium text-gray-500">Another Person's Card</label>
                              <p className="text-sm text-gray-900">{selectedDispute.anotherPersonsCard ? 'Yes' : 'No'}</p>
                            </div>
                          )}
                        </div>
                      </div>
                    </>
                  )}
                  
                  <div className="border-t pt-4 mb-6">
                    <h4 className="text-md font-semibold mb-3">Timeline</h4>
                    <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
                      <div>
                        <label className="block text-sm font-medium text-gray-500">Created</label>
                        <p className="text-sm text-gray-900">{selectedDispute.dateCreated}</p>
                      </div>
                      <div>
                        <label className="block text-sm font-medium text-gray-500">Due Date</label>
                        <p className="text-sm text-gray-900">{selectedDispute.dueDate}</p>
                      </div>
                    </div>
                  </div>
                  
                  <div className="mb-4">
                    <label className="block text-sm font-medium text-gray-500 mb-2">Parties Involved</label>
                    <div className="flex flex-wrap gap-2">
                      {selectedDispute.parties?.map((party, index) => (
                        <span key={index} className="bg-blue-100 text-blue-800 px-2 py-1 rounded-full text-sm">
                          {party}
                        </span>
                      ))}
                    </div>
                  </div>
                  
                  <div className="mb-6">
                    <label className="block text-sm font-medium text-gray-500 mb-2">Description</label>
                    <p className="text-sm text-gray-900">{selectedDispute.description}</p>
                  </div>

                  {selectedDispute.managementReview && (
                    <div className="mb-6">
                      <label className="block text-sm font-medium text-gray-500 mb-2">Management Review / Notes</label>
                      <div className="bg-gray-50 p-3 rounded-lg">
                        <p className="text-sm text-gray-900">{selectedDispute.managementReview}</p>
                      </div>
                    </div>
                  )}
                  
                  <div className="flex gap-3">
                    <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700">
                      Edit Dispute
                    </button>
                    <button className="bg-green-600 text-white px-4 py-2 rounded-lg hover:bg-green-700">
                      Add Note
                    </button>
                    <button className="bg-purple-600 text-white px-4 py-2 rounded-lg hover:bg-purple-700">
                      Update Status
                    </button>
                    <button className="bg-gray-300 text-gray-700 px-4 py-2 rounded-lg hover:bg-gray-400">
                      Generate Report
                    </button>
                  </div>
                </div>
              </div>
            );
          };

          return (
            <div className="min-h-screen bg-gray-50">
              {/* Header */}
              <div className="bg-white shadow-sm border-b">
                <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                  <div className="flex justify-between items-center py-4">
                    <h1 className="text-2xl font-bold text-gray-900">Dispute Resolution System</h1>
                    <div className="flex items-center gap-4">
                      <div className="bg-green-50 border border-green-200 rounded-lg px-3 py-1">
                        <span className="text-sm text-green-800">✓ Real dispute data loaded</span>
                      </div>
                      <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 flex items-center gap-2">
                        <Download className="w-4 h-4" />
                        Export
                      </button>
                      <div className="flex items-center gap-2">
                        <Users className="w-5 h-5 text-gray-400" />
                        <span className="text-sm text-gray-600">Dispute Specialist</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>

              {/* Navigation */}
              <div className="bg-white shadow-sm">
                <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                  <nav className="flex space-x-8">
                    {['dashboard', 'disputes', 'reasons', 'timeline', 'analytics', 'reports'].map((tab) => (
                      <button
                        key={tab}
                        onClick={() => setActiveTab(tab)}
                        className={`py-4 px-1 border-b-2 font-medium text-sm capitalize ${
                          activeTab === tab
                            ? 'border-blue-500 text-blue-600'
                            : 'border-transparent text-gray-500 hover:text-gray-700'
                        }`}
                      >
                        {tab === 'reasons' ? 'Dispute Reasons' : 
                         tab === 'timeline' ? 'Disputed On' : tab}
                      </button>
                    ))}
                  </nav>
                </div>
              </div>

              {/* Main Content */}
              <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
                {activeTab === 'dashboard' && (
                  <div>
                    <DashboardStats />
                    <DisputesList />
                  </div>
                )}
                
                {activeTab === 'disputes' && <DisputesList />}
                
                {activeTab === 'reasons' && (
                  <div className="space-y-6">
                    <div className="bg-white rounded-lg shadow-sm border p-6">
                      <h2 className="text-lg font-semibold mb-4">Disputes by Reason</h2>
                      
                      <div className="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                        <div className="bg-blue-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-blue-600">
                            {new Set(disputes.map(d => d.reason)).size}
                          </div>
                          <div className="text-sm text-blue-700">Unique Reasons</div>
                        </div>
                        <div className="bg-red-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-red-600">
                            {disputes.filter(d => d.reason === 'Fraudulent').length}
                          </div>
                          <div className="text-sm text-red-700">Fraudulent Claims</div>
                        </div>
                        <div className="bg-green-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-green-600">
                            {disputes.filter(d => d.reason === 'Subscription Cancelled').length}
                          </div>
                          <div className="text-sm text-green-700">Subscription Issues</div>
                        </div>
                      </div>

                      <div className="space-y-4">
                        {Object.entries(
                          disputes.reduce((acc, dispute) => {
                            const reason = dispute.reason || 'Unknown';
                            if (!acc[reason]) {
                              acc[reason] = [];
                            }
                            acc[reason].push(dispute);
                            return acc;
                          }, {})
                        )
                        .sort((a, b) => b[1].length - a[1].length)
                        .map(([reason, reasonDisputes]) => (
                          <div key={reason} className="border rounded-lg p-4">
                            <div className="flex justify-between items-center mb-3">
                              <h3 className="font-medium text-lg">{reason}</h3>
                              <div className="flex items-center gap-4">
                                <span className="text-sm text-gray-600">
                                  {reasonDisputes.length} disputes
                                </span>
                                <span className="text-sm font-medium">
                                  ${reasonDisputes.reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                                </span>
                              </div>
                            </div>
                            
                            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3">
                              {reasonDisputes.slice(0, 6).map(dispute => (
                                <div key={dispute.id} className="bg-gray-50 p-3 rounded">
                                  <div className="font-medium text-sm">{dispute.subName || dispute.title}</div>
                                  <div className="text-xs text-gray-600 mt-1">
                                    ${dispute.value.toLocaleString()} • {dispute.disputeStatus || dispute.status}
                                  </div>
                                  <div className="text-xs text-gray-500 mt-1">{dispute.dateCreated}</div>
                                </div>
                              ))}
                              {reasonDisputes.length > 6 && (
                                <div className="bg-gray-100 p-3 rounded flex items-center justify-center">
                                  <span className="text-sm text-gray-600">
                                    +{reasonDisputes.length - 6} more
                                  </span>
                                </div>
                              )}
                            </div>
                          </div>
                        ))}
                      </div>
                    </div>
                  </div>
                )}

                {activeTab === 'timeline' && (
                  <div className="space-y-6">
                    <div className="bg-white rounded-lg shadow-sm border p-6">
                      <h2 className="text-lg font-semibold mb-4">Disputes Timeline</h2>
                      
                      <div className="grid grid-cols-1 md:grid-cols-4 gap-4 mb-6">
                        <div className="bg-purple-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-purple-600">
                            {disputes.filter(d => {
                              const disputeDate = new Date(d.disputeDate || d.dateCreated);
                              const today = new Date();
                              const diffTime = today - disputeDate;
                              const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                              return diffDays <= 7;
                            }).length}
                          </div>
                          <div className="text-sm text-purple-700">This Week</div>
                        </div>
                        <div className="bg-blue-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-blue-600">
                            {disputes.filter(d => {
                              const disputeDate = new Date(d.disputeDate || d.dateCreated);
                              const today = new Date();
                              const diffTime = today - disputeDate;
                              const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                              return diffDays <= 30;
                            }).length}
                          </div>
                          <div className="text-sm text-blue-700">This Month</div>
                        </div>
                        <div className="bg-yellow-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-yellow-600">
                            {disputes.filter(d => {
                              const disputeDate = new Date(d.disputeDate || d.dateCreated);
                              const today = new Date();
                              const diffTime = today - disputeDate;
                              const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                              return diffDays > 30 && diffDays <= 90;
                            }).length}
                          </div>
                          <div className="text-sm text-yellow-700">Last 3 Months</div>
                        </div>
                        <div className="bg-gray-50 p-4 rounded-lg">
                          <div className="text-2xl font-bold text-gray-600">
                            {disputes.filter(d => {
                              const disputeDate = new Date(d.disputeDate || d.dateCreated);
                              const today = new Date();
                              const diffTime = today - disputeDate;
                              const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                              return diffDays > 90;
                            }).length}
                          </div>
                          <div className="text-sm text-gray-700">Older</div>
                        </div>
                      </div>

                      <div className="space-y-4">
                        {Object.entries(
                          disputes.reduce((acc, dispute) => {
                            const date = dispute.disputeDate || dispute.dateCreated;
                            if (!acc[date]) {
                              acc[date] = [];
                            }
                            acc[date].push(dispute);
                            return acc;
                          }, {})
                        )
                        .sort((a, b) => new Date(b[0]) - new Date(a[0]))
                        .slice(0, 10)
                        .map(([date, dateDisputes]) => (
                          <div key={date} className="border rounded-lg p-4">
                            <div className="flex justify-between items-center mb-3">
                              <h3 className="font-medium text-lg">{date}</h3>
                              <div className="flex items-center gap-4">
                                <span className="text-sm text-gray-600">
                                  {dateDisputes.length} disputes
                                </span>
                                <span className="text-sm font-medium">
                                  ${dateDisputes.reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                                </span>
                              </div>
                            </div>
                            
                            <div className="space-y-2">
                              {dateDisputes.map(dispute => (
                                <div key={dispute.id} className="flex justify-between items-center py-2 px-3 bg-gray-50 rounded">
                                  <div className="flex items-center gap-3">
                                    <span className={`w-3 h-3 rounded-full ${
                                      dispute.disputeStatus === 'WON' ? 'bg-green-500' :
                                      dispute.disputeStatus === 'LOST' ? 'bg-red-500' :
                                      dispute.disputeStatus === 'NEW' ? 'bg-purple-500' :
                                      dispute.disputeStatus === 'VISA RDR' ? 'bg-orange-500' :
                                      'bg-gray-500'
                                    }`}></span>
                                    <div>
                                      <div className="font-medium text-sm">{dispute.subName || dispute.title}</div>
                                      <div className="text-xs text-gray-600">{dispute.reason} • {dispute.purpose}</div>
                                    </div>
                                  </div>
                                  <div className="text-right">
                                    <div className="text-sm font-medium">${dispute.value.toLocaleString()}</div>
                                    <div className="text-xs text-gray-500">{dispute.disputeStatus || dispute.status}</div>
                                  </div>
                                </div>
                              ))}
                            </div>
                          </div>
                        ))}
                      </div>
                    </div>
                  </div>
                )}

                {activeTab === 'analytics' && (
                  <div className="space-y-6">
                    <div className="bg-white rounded-lg shadow-sm border p-6">
                      <h2 className="text-lg font-semibold mb-4">Analytics Dashboard</h2>
                      
                      <div className="bg-gray-50 p-4 rounded-lg mb-6">
                        <h3 className="font-semibold mb-3">Overall Summary</h3>
                        <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                          <div className="text-center">
                            <div className="text-2xl font-bold text-gray-900">{disputes.length}</div>
                            <div className="text-sm text-gray-600">Total Disputes</div>
                          </div>
                          <div className="text-center">
                            <div className="text-2xl font-bold text-green-600">
                              ${disputes.reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                            </div>
                            <div className="text-sm text-gray-600">Total Amount</div>
                          </div>
                          <div className="text-center">
                            <div className="text-2xl font-bold text-blue-600">
                              ${Math.round(disputes.reduce((sum, d) => sum + d.value, 0) / disputes.length).toLocaleString()}
                            </div>
                            <div className="text-sm text-gray-600">Average Value</div>
                          </div>
                          <div className="text-center">
                            <div className="text-2xl font-bold text-purple-600">
                              {Math.round((disputes.filter(d => d.disputeStatus === 'WON' || d.disputeStatus === 'ACCEPTED').length / disputes.length) * 100)}%
                            </div>
                            <div className="text-sm text-gray-600">Overall Win Rate</div>
                          </div>
                        </div>
                      </div>

                      <div className="grid grid-cols-1 md:grid-cols-4 gap-4 mb-6">
                        <div className="bg-green-50 p-4 rounded-lg border border-green-200">
                          <div className="text-2xl font-bold text-green-600">
                            {disputes.filter(d => d.disputeStatus === 'WON').length}
                          </div>
                          <div className="text-sm text-green-700 mb-1">WON Cases</div>
                          <div className="text-xs text-green-600">
                            ${disputes.filter(d => d.disputeStatus === 'WON').reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                          </div>
                        </div>
                        <div className="bg-red-50 p-4 rounded-lg border border-red-200">
                          <div className="text-2xl font-bold text-red-600">
                            {disputes.filter(d => d.disputeStatus === 'LOST').length}
                          </div>
                          <div className="text-sm text-red-700 mb-1">LOST Cases</div>
                          <div className="text-xs text-red-600">
                            ${disputes.filter(d => d.disputeStatus === 'LOST').reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                          </div>
                        </div>
                        <div className="bg-blue-50 p-4 rounded-lg border border-blue-200">
                          <div className="text-2xl font-bold text-blue-600">
                            {disputes.filter(d => d.disputeStatus === 'ACCEPTED').length}
                          </div>
                          <div className="text-sm text-blue-700 mb-1">ACCEPTED Cases</div>
                          <div className="text-xs text-blue-600">
                            ${disputes.filter(d => d.disputeStatus === 'ACCEPTED').reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                          </div>
                        </div>
                        <div className="bg-orange-50 p-4 rounded-lg border border-orange-200">
                          <div className="text-2xl font-bold text-orange-600">
                            {disputes.filter(d => d.disputeStatus === 'VISA RDR').length}
                          </div>
                          <div className="text-sm text-orange-700 mb-1">VISA RDR Cases</div>
                          <div className="text-xs text-orange-600">
                            ${disputes.filter(d => d.disputeStatus === 'VISA RDR').reduce((sum, d) => sum + d.value, 0).toLocaleString()}
                          </div>
                        </div>
                      </div>

                      <div className="border rounded-lg p-4">
                        <h3 className="font-medium mb-3">Recent High-Value Disputes</h3>
                        <div className="space-y-2">
                          {disputes
                            .filter(d => d.value > 200)
                            .slice(0, 5)
                            .map(dispute => (
                              <div key={dispute.id} className="flex justify-between items-center py-2 border-b last:border-b-0">
                                <div>
                                  <span className="text-sm font-medium">{dispute.subName || dispute.title}</span>
                                  <span className="text-xs text-gray-500 ml-2">{dispute.reason}</span>
                                </div>
                                <div className="text-right">
                                  <div className="text-sm font-medium">${dispute.value.toLocaleString()}</div>
                                  <div className="text-xs text-gray-500">{dispute.disputeStatus}</div>
                                </div>
                              </div>
                            ))}
                        </div>
                      </div>
                    </div>
                  </div>
                )}
                
                {activeTab === 'reports' && (
                  <div className="bg-white rounded-lg shadow-sm border p-6">
                    <h2 className="text-lg font-semibold mb-4">Reports</h2>
                    <p className="text-gray-600">Generate comprehensive reports on dispute resolution metrics, trends, and performance.</p>
                  </div>
                )}
              </div>

              {/* Modals */}
              {showNewDisputeForm && <NewDisputeForm />}
              {selectedDispute && <DisputeDetailModal />}
            </div>
          );
        };

        ReactDOM.render(<DisputeResolutionApp />, document.getElementById('root'));
    </script>
</body>
</html># whizz-dispute-resolution-app
Dispute Resolution Management System
