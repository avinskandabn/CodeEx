# CodeEx
Test
import React from "react";
import {
  BarChart,
  Bar,
  XAxis,
  YAxis,
  Tooltip,
  CartesianGrid,
  Legend,
  ResponsiveContainer,
  LabelList,
} from "recharts";

type InfraDataType = {
  name: string;
  embodied: number;
  operational: number;
};

type ResourceDataType = {
  name: string;
  emissions: number;
};

interface EmissionChartsProps {
  infraData: InfraDataType[];
  resourceData: ResourceDataType[];
}

const EmissionCharts: React.FC<EmissionChartsProps> = ({ infraData, resourceData }) => {
  return (
    <div style={{ display: "flex", gap: "2rem", flexWrap: "wrap" }}>
      {/* Chart 1 - Breakdown by infrastructural components */}
      <div style={{ flex: "1 1 500px", height: 400 }}>
        <h3>Breakdown by infrastructural components</h3>
        <ResponsiveContainer width="100%" height="100%">
          <BarChart
            data={infraData}
            margin={{ top: 20, right: 20, left: 0, bottom: 0 }}
          >
            <CartesianGrid strokeDasharray="3 3" />
            <XAxis dataKey="name" />
            <YAxis
              label={{
                value: "CO₂ emissions (kg)",
                angle: -90,
                position: "insideLeft",
              }}
            />
            <Tooltip formatter={(value) => `${value} kg`} />
            <Legend />
            <Bar dataKey="embodied" fill="#72c7d6" name="Embodied emissions">
              <LabelList position="top" formatter={(v) => `${v}`} />
            </Bar>
            <Bar dataKey="operational" fill="#d6d672" name="Operational emissions">
              <LabelList position="top" formatter={(v) => `${v}`} />
            </Bar>
          </BarChart>
        </ResponsiveContainer>
      </div>

      {/* Chart 2 - Breakdown by resources */}
      <div style={{ flex: "1 1 500px", height: 400 }}>
        <h3>Breakdown by resources</h3>
        <ResponsiveContainer width="100%" height="100%">
          <BarChart
            data={resourceData}
            margin={{ top: 20, right: 20, left: 0, bottom: 0 }}
          >
            <CartesianGrid strokeDasharray="3 3" />
            <XAxis dataKey="name" />
            <YAxis
              label={{
                value: "CO₂ emissions (kg)",
                angle: -90,
                position: "insideLeft",
              }}
            />
            <Tooltip formatter={(value) => `${value} kg`} />
            <Bar dataKey="emissions" fill="#00a6ff" name="Emissions">
              <LabelList position="top" formatter={(v) => `${v}`} />
            </Bar>
          </BarChart>
        </ResponsiveContainer>
      </div>
    </div>
  );
};

export default EmissionCharts;


import React, { useEffect, useState } from "react";
import EmissionCharts from "./EmissionCharts";

function App() {
  const [infraData, setInfraData] = useState([]);
  const [resourceData, setResourceData] = useState([]);

  useEffect(() => {
    // Example API fetch (replace with your real API)
    fetch("/api/emissions")
      .then((res) => res.json())
      .then((data) => {
        setInfraData(data.infrastructure);
        setResourceData(data.resources);
      });
  }, []);

  return (
    <div style={{ padding: "2rem" }}>
      <EmissionCharts infraData={infraData} resourceData={resourceData} />
    </div>
  );
}




export default App;


import { BarChart, Bar, XAxis, YAxis, Tooltip } from "recharts";

const data = [
  { name: "Data Centers", value: 14000 },
  { name: "Networks", value: 15000 },
  { name: "Devices", value: 25000 }
];

// Custom Chimney + Smoke Shape
const ChimneyBar = (props: any) => {
  const { x, y, width, height, fill } = props;
  return (
    <g>
      {/* Chimney body */}
      <rect x={x} y={y} width={width} height={height} fill={fill} rx={4} />

      {/* Smoke (simple circles rising) */}
      <circle cx={x + width / 2} cy={y - 10} r={6} fill="lightgray" opacity={0.7} />
      <circle cx={x + width / 2} cy={y - 25} r={10} fill="gray" opacity={0.5} />
      <circle cx={x + width / 2} cy={y - 45} r={14} fill="darkgray" opacity={0.3} />
    </g>
  );
};

export default function ChimneyChart() {
  return (
    <BarChart width={600} height={400} data={data} layout="vertical">
      <XAxis type="number" />
      <YAxis dataKey="name" type="category" />
      <Tooltip />
      <Bar dataKey="value" shape={<ChimneyBar />} fill="#8884d8" />
    </BarChart>
  );




  new   



  import React from "react";
import {
  BarChart,
  Bar,
  XAxis,
  YAxis,
  CartesianGrid,
  Tooltip,
  ResponsiveContainer,
} from "recharts";

const ChimneyShape = ({ x, y, width, height, fill }: any) => {
  const chimneyTop = x + width / 2;
  return (
    <g>
      {/* Chimney trapezoid (narrow top, wide bottom) */}
      <polygon
        points={`
          ${x},${y + height} 
          ${x + width},${y + height} 
          ${x + width * 0.8},${y} 
          ${x + width * 0.2},${y}
        `}
        fill={fill}
      />

      {/* Smoke bubbles */}
      <circle cx={chimneyTop} cy={y - 10} r={8} fill="gray" opacity={0.6} />
      <circle cx={chimneyTop + 10} cy={y - 25} r={12} fill="gray" opacity={0.5} />
      <circle cx={chimneyTop - 15} cy={y - 45} r={16} fill="gray" opacity={0.4} />
    </g>
  );
};

const data = [
  { name: "Data Centres", value: 14000 },
  { name: "Network", value: 15000 },
  { name: "Devices", value: 25000 },
];

export default function ChimneyChart() {
  return (
    <ResponsiveContainer width="100%" height={400}>
      <BarChart data={data}>
        <CartesianGrid strokeDasharray="3 3" />
        <XAxis dataKey="name" />
        <YAxis />
        <Tooltip />

        {/* Use custom chimney shape here */}
        <Bar dataKey="value" fill="#3CB371" shape={<ChimneyShape />} />
      </BarChart>
    </ResponsiveContainer>
  );
}


