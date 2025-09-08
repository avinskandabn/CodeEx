import React from "react";
import {
  PieChart,
  Pie,
  Cell,
  ResponsiveContainer,
  Label
} from "recharts";

const data = [
  { name: "Complied", value: 50 },
  { name: "Pending", value: 17 },
];

const COLORS = ["#28a745", "#dc3545"]; // green and red

const ComplianceDonut: React.FC = () => {
  const total = data.reduce((sum, item) => sum + item.value, 0);

  return (
    <ResponsiveContainer width={300} height={300}>
      <PieChart>
        <Pie
          data={data}
          innerRadius={80}
          outerRadius={120}
          paddingAngle={2}
          dataKey="value"
        >
          {data.map((_, index) => (
            <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
          ))}
          {/* Center text */}
          <Label
            position="center"
            content={({ viewBox }) => {
              if (viewBox && "cx" in viewBox && "cy" in viewBox) {
                return (
                  <text
                    x={viewBox.cx}
                    y={viewBox.cy}
                    textAnchor="middle"
                    dominantBaseline="middle"
                    fontSize={20}
                    fill="#000"
                  >
                    <tspan x={viewBox.cx} dy="-0.6em" fontSize={16}>
                      Total
                    </tspan>
                    <tspan x={viewBox.cx} dy="1.2em" fontSize={28} fontWeight="bold">
                      {total}
                    </tspan>
                  </text>
                );
              }
              return null;
            }}
          />
        </Pie>
      </PieChart>
    </ResponsiveContainer>
  );
};

export default ComplianceDonut;
