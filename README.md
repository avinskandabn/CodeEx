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
