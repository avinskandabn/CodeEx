import React from "react";
import "./ComplexityCard.scss";

export type Variant = "green" | "red";

export interface RowData {
  fileName: string;
  complexity: string;
}

interface Props {
  title: string;
  variant: Variant; // "green" (lowest) or "red" (highest)
  rows: RowData[];
  width?: number;   // optional (px)
  height?: number;  // optional (px)
}

const ComplexityCard: React.FC<Props> = ({
  title,
  variant,
  rows,
  width = 420,
  height = 270,
}) => {
  return (
    <div
      className={`complexity-card ${variant}`}
      style={{ width, height }}
      data-variant={variant}
    >
      {/* Layer 1: back color polygon band */}
      <div className="band" />

      {/* Layer 2: white rectangle body */}
      <div className="body" />

      {/* Layer 3: polygon label/header */}
      <div className="label">{title}</div>

      {/* Table content */}
      <table className="table">
        <thead>
          <tr>
            <th>File name</th>
            <th>Complexity</th>
          </tr>
        </thead>
        <tbody>
          {rows.map((r, i) => (
            <tr key={`${r.fileName}-${i}`}>
              <td>{r.fileName}</td>
              <td>{r.complexity}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default ComplexityCard;

.complexity-card {
  position: relative;
  border-radius: 12px;
  overflow: visible; // we want the header to float a little
  font-family: Inter, Arial, sans-serif;

  // Layer 1: back polygon color band
  .band {
    position: absolute;
    inset: 0;
    z-index: 0;
    border-radius: 12px;

    // the right color strip with an angled “head”
    &::before {
      content: "";
      position: absolute;
      right: 0;
      top: 0;
      width: 36%;
      height: 92%;
      border-bottom-right-radius: 12px;
      border-bottom-left-radius: 4px;
      // angled head (this shape is what you pointed out)
      clip-path: polygon(16% 0, 100% 0, 100% 100%, 0 100%, 0 16%);
    }
  }

  // Layer 2: the white rectangle body
  .body {
    position: absolute;
    inset: 10px;
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, .06);
    border: 1px solid #e6e6ea;
    z-index: 1;
  }

  // Layer 3: polygon header/label
  .label {
    position: absolute;
    right: 10px;
    top: -2px;
    height: 46px;
    line-height: 46px;
    padding: 0 16px;
    color: #fff;
    font-weight: 700;
    border-top-right-radius: 12px;
    border-top-left-radius: 10px;
    z-index: 2;
    letter-spacing: .2px;
    // polygon tail to mimic the screenshot
    clip-path: polygon(0 0, 100% 0, 100% 76%, 86% 76%, 76% 100%, 0 100%);
  }

  // Table inside the card
  .table {
    position: absolute;
    inset: 56px 18px 18px 18px;
    width: calc(100% - 36px);
    border-collapse: collapse;
    font-size: 14px;

    thead th {
      text-align: left;
      padding: 8px 10px;
      border-bottom: 1px solid #e9e9ee;
      color: #333;
    }

    tbody td {
      padding: 12px 10px;
      border-bottom: 1px solid #f0f0f4;
      color: #444;
    }

    tr:last-child td {
      border-bottom: 0;
    }

    // subtle column divider like your screenshot
    th:first-child, td:first-child {
      border-right: 1px solid #efeff4;
    }
  }

  // Color variants (match both band and label)
  &.green {
    .band { background: #e8f6ee; }
    .band::before, .label { background: #3abf6f; } // green
  }

  &.red {
    .band { background: #fdeceb; }
    .band::before, .label { background: #e65b53; } // red
  }
}



import React from "react";
import ComplexityCard, { RowData } from "./ComplexityCard";
import "./ComplexityPair.scss";

interface Props {
  lowest: RowData[];
  highest: RowData[];
}

const ComplexityPair: React.FC<Props> = ({ lowest, highest }) => {
  return (
    <div className="pair-wrap">
      <ComplexityCard
        title="Lowest complexities"
        variant="green"
        rows={lowest}
      />
      <ComplexityCard
        title="Highest complexities"
        variant="red"
        rows={highest}
      />
    </div>
  );
};

export default ComplexityPair;



// In some page or container
const rows = [
  { fileName: "Aboutus123.java", complexity: "O(n)" },
  { fileName: "Aboutus123.java", complexity: "O(n)" },
  { fileName: "Aboutus123.java", complexity: "O(n)" },
];

<ComplexityPair lowest={rows} highest={rows} />;




