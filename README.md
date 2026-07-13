<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VanSecure | Fleet Downtime & True Theft Cost Calculator</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        /* Custom range slider styling override for a premium look */
        input[type="range"] {
            accent-color: #dc2626;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 font-sans min-h-screen flex items-center justify-center p-4 sm:p-6">

    <div class="w-full max-w-5xl bg-slate-900 border border-slate-800 rounded-2xl shadow-2xl overflow-hidden grid grid-cols-1 lg:grid-cols-12">
        
        <!-- INPUT CONTROLS PANEL -->
        <div class="lg:col-span-5 p-6 sm:p-8 bg-slate-900/50 border-b lg:border-b-0 lg:border-r border-slate-800 space-y-6">
            <div>
                <span class="text-xs font-semibold tracking-wider text-red-500 uppercase">VanSecure Risk Tool</span>
                <h2 class="text-2xl font-bold text-white mt-1">Fleet Impact Simulator</h2>
                <p class="text-slate-400 text-sm mt-1">Adjust the operational parameters below to reveal the true cost of vehicle downtime.</p>
            </div>

            <hr class="border-slate-800">

            <div class="space-y-5">
                <!-- Vans Targeted -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="vans" class="font-medium text-slate-300">Vans Cleared Out Out</label>
                        <span id="vansVal" class="font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">1</span>
                    </div>
                    <input type="range" id="vans" min="1" max="10" value="1" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Days Idle -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="days" class="font-medium text-slate-300">Days Idle (Waiting for Repair)</label>
                        <span id="daysVal" class="font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">4 days</span>
                    </div>
                    <input type="range" id="days" min="1" max="14" value="4" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Daily Engineer Revenue -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="revenue" class="font-medium text-slate-300">Daily Lost Revenue (Per Van)</label>
                        <div class="flex items-center gap-1 font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">
                            <span>£</span><span id="revenueVal">500</span>
                        </div>
                    </div>
                    <input type="range" id="revenue" min="100" max="1500" step="50" value="500" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Tool Replacement Shortfall -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="tools" class="font-medium text-slate-300">Tool Replacement Shortfall</label>
                        <div class="flex items-center gap-1 font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">
                            <span>£</span><span id="toolsVal">1,200</span>
                        </div>
                    </div>
                    <input type="range" id="tools" min="0" max="5000" step="100" value="1200" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Insurance Excess -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="excess" class="font-medium text-slate-300">Insurance Excess Fee</label>
                        <div class="flex items-center gap-1 font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">
                            <span>£</span><span id="excessVal">250</span>
                        </div>
                    </div>
                    <input type="range" id="excess" min="0" max="1000" step="50" value="250" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Reactive Hire Van Cost -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="hire" class="font-medium text-slate-300">Daily Hire Van Cost</label>
                        <div class="flex items-center gap-1 font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">
                            <span>£</span><span id="hireVal">90</span>
                        </div>
                    </div>
                    <input type="range" id="hire" min="0" max="200" step="10" value="90" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>

                <!-- Contract Penalty -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center text-sm">
                        <label for="penalty" class="font-medium text-slate-300">SLA / Contract Penalty Fee</label>
                        <div class="flex items-center gap-1 font-bold text-white px-2 py-0.5 bg-slate-800 rounded-md border border-slate-700">
                            <span>£</span><span id="penaltyVal">500</span>
                        </div>
                    </div>
                    <input type="range" id="penalty" min="0" max="2500" step="100" value="500" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer">
                </div>
            </div>
        </div>

        <!-- VISUALIZATION DASHBOARD PANEL -->
        <div class="lg:col-span-7 p-6 sm:p-8 bg-slate-950 flex flex-col justify-between space-y-8">
            
            <!-- MAIN KPI READOUT -->
            <div class="bg-gradient-to-br from-slate-900 to-slate-900/40 p-6 rounded-xl border border-slate-800 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                <div>
                    <h3 class="text-sm font-medium text-slate-400">Total Cash Flow Impact</h3>
                    <div class="text-4xl sm:text-5xl font-black text-red-500 mt-1 tracking-tight">£<span id="totalLoss">4,110</span></div>
                </div>
                <div class="text-xs sm:text-right text-slate-400 max-w-xs">
                    <p class="font-semibold text-white">The Business Continuity Gap</p>
                    <p class="mt-0.5">Your true loss is <span id="gapMultiplier" class="text-red-400 font-bold">3.4x</span> higher than just the uninsured tool value.</p>
                </div>
            </div>

            <!-- THE DYNAMIC BAR CHART CONTAINER -->
            <div class="space-y-6 flex-grow flex flex-col justify-center">
                <h4 class="text-sm font-bold text-slate-300 uppercase tracking-wider">Financial Breakdown</h4>
                
                <div class="space-y-4">
                    <!-- Direct Hardware Costs -->
                    <div class="space-y-1.5">
                        <div class="flex justify-between text-xs font-medium">
                            <span class="text-slate-400">Direct Equipment Losses (Tools + Excess)</span>
                            <span class="text-white font-bold">£<span id="directLabel">1,450</span></span>
                        </div>
                        <div class="w-full h-5 bg-slate-900 rounded-md overflow-hidden border border-slate-800">
                            <div id="directBar" class="h-full bg-slate-500 transition-all duration-150 ease-out" style="width: 35%"></div>
                        </div>
                    </div>

                    <!-- Hidden Operational Downtime Costs -->
                    <div class="space-y-1.5">
                        <div class="flex justify-between text-xs font-medium">
                            <span class="text-red-400 font-semibold flex items-center gap-1">
                                <span>●</span> Hidden Operational Downtime Costs
                            </span>
                            <span class="text-red-500 font-bold">£<span id="hiddenLabel">2,660</span></span>
                        </div>
                        <div class="w-full h-5 bg-slate-900 rounded-md overflow-hidden border border-slate-800">
                            <div id="hiddenBar" class="h-full bg-red-600 transition-all duration-150 ease-out" style="width: 65%"></div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- FOOTER INSIGHT / CALL TO ACTION -->
            <div class="border-t border-slate-900 pt-6 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 text-xs text-slate-400">
                <blockquote class="border-l-2 border-red-500 pl-3 italic">
                    "If your security layout doesn't fit your fleet's daily schedule, you're not managing risk—you're just buying boxes of hardware."
                </blockquote>
                <a href="https://vansecure.co.uk" target="_blank" class="w-full sm:w-auto text-center px-4 py-2.5 bg-red-600 hover:bg-red-700 active:bg-red-800 text-white font-bold rounded-lg transition-colors shadow-lg shadow-red-900/20 whitespace-nowrap">
                    Book Risk Assessment
                </a>
            </div>

        </div>
    </div>

    <!-- CALCULATION LOGIC ENGINE -->
    <script>
        const inputs = ['vans', 'days', 'revenue', 'tools', 'excess', 'hire', 'penalty'];
        
        function formatNum(num) {
            return num.toLocaleString('en-GB');
        }

        function calculateMetrics() {
            // Retrieve current slider values
            const vans = parseInt(document.getElementById('vans').value);
            const days = parseInt(document.getElementById('days').value);
            const revenue = parseInt(document.getElementById('revenue').value);
            const tools = parseInt(document.getElementById('tools').value);
            const excess = parseInt(document.getElementById('excess').value);
            const hire = parseInt(document.getElementById('hire').value);
            const penalty = parseInt(document.getElementById('penalty').value);

            // Update visible input badge readouts
            document.getElementById('vansVal').textContent = vans;
            document.getElementById('daysVal').textContent = days === 1 ? '1 day' : `${days} days`;
            document.getElementById('revenueVal').textContent = formatNum(revenue);
            document.getElementById('toolsVal').textContent = formatNum(tools);
            document.getElementById('excessVal').textContent = formatNum(excess);
            document.getElementById('hireVal').textContent = formatNum(hire);
            document.getElementById('penaltyVal').textContent = formatNum(penalty);

            // Math execution
            const directCosts = (tools + excess) * vans;
            const hiddenCosts = ((revenue * days) + (hire * days) + penalty) * vans;
            const totalCost = directCosts + hiddenCosts;

            // Calculate business continuity gap multiplier
            const baseEquipmentValue = tools > 0 ? tools * vans : 1; 
            const multiplier = (totalCost / baseEquipmentValue).toFixed(1);

            // Update UI KPI counters
            document.getElementById('totalLoss').textContent = formatNum(totalCost);
            document.getElementById('directLabel').textContent = formatNum(directCosts);
            document.getElementById('hiddenLabel').textContent = formatNum(hiddenCosts);
            document.getElementById('gapMultiplier').textContent = `${multiplier}x`;

            // Calculate chart percentages to avoid clipping/overflow
            const maxCalculatedSegment = Math.max(directCosts, hiddenCosts, 1);
            const directBarPct = Math.max((directCosts / (directCosts + hiddenCosts)) * 100, 2);
            const hiddenBarPct = Math.max((hiddenCosts / (directCosts + hiddenCosts)) * 100, 2);

            // Update graphical bar widths dynamically
            document.getElementById('directBar').style.width = `${directBarPct}%`;
            document.getElementById('hiddenBar').style.width = `${hiddenBarPct}%`;
        }

        // Attach dynamic listener triggers to every input control
        inputs.forEach(id => {
            document.getElementById(id).addEventListener('input', calculateMetrics);
        });

        // Initialize simulation values on load
        calculateMetrics();
    </script>
</body>
</html>
