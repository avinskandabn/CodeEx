import React from "react";
import "./ComplexityTables.scss";

interface RowData {
  fileName: string;
  complexity: string;
}

interface Props {
  highest: RowData[];
  lowest: RowData[];
}

const ComplexityTables: React.FC<Props> = ({ highest, lowest }) => {
  return (
    <div className="tables-container">
      {/* Lowest Complexity Table (Green) */}
      <div className="complexity-card green">
        <div className="header-bar">
          <span className="header-text">Lowest complexities</span>
          <span className="arrow">↓</span>
        </div>
        <table className="complexity-table">
          <thead>
            <tr>
              <th>File name</th>
              <th>Complexity</th>
            </tr>
          </thead>
          <tbody>
            {lowest.map((row, i) => (
              <tr key={i}>
                <td>{row.fileName}</td>
                <td>{row.complexity}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>

      {/* Highest Complexity Table (Red) */}
      <div className="complexity-card red">
        <div className="header-bar">
          <span className="header-text">Highest complexities</span>
          <span className="arrow">↑</span>
        </div>
        <table className="complexity-table">
          <thead>
            <tr>
              <th>File name</th>
              <th>Complexity</th>
            </tr>
          </thead>
          <tbody>
            {highest.map((row, i) => (
              <tr key={i}>
                <td>{row.fileName}</td>
                <td>{row.complexity}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
};

export default ComplexityTables;







.tables-container {
  display: flex;
  gap: 20px;
}

.complexity-card {
  width: 400px;
  border: 1px solid #ddd;
  border-radius: 6px;
  overflow: hidden;
  font-family: Arial, sans-serif;
  background: white;
  box-shadow: 0 2px 6px rgba(0,0,0,0.1);

  .header-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 15px;
    font-weight: bold;
    color: white;

    .arrow {
      font-size: 18px;
    }
  }

  &.green .header-bar {
    background: #2ecc71; // green
  }

  &.red .header-bar {
    background: #e74c3c; // red
  }

  .complexity-table {
    width: 100%;
    border-collapse: collapse;

    th {
      text-align: left;
      padding: 8px 12px;
      border-bottom: 1px solid #ddd;
      font-size: 14px;
      background: #f9f9f9;
    }

    td {
      padding: 8px 12px;
      border-bottom: 1px solid #f1f1f1;
      font-size: 14px;
    }

    tr:last-child td {
      border-bottom: none;
    }
  }
}




import React from "react";
import ComplexityTables from "./ComplexityTables";

const highest = [
  { fileName: "Aboutus123.java", complexity: "O(n)" },
  { fileName: "Aboutus123.java", complexity: "O(n)" },
  { fileName: "Aboutus123.java", complexity: "O(n)" }
];

const lowest = [
  { fileName: "Aboutus123.java", complexity: "O(n)" },
  { fileName: "Aboutus123.java", complexity: "O(n)" },
  { fileName: "Aboutus123.java", complexity: "O(n)" }
];

function App() {
  return <ComplexityTables highest={highest} lowest={lowest} />;
}

export default App;



